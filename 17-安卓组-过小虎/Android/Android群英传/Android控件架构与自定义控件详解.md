[toc]


<font size = "4">

### Android控件架构
安卓的控件分为**ViewGroup**和**View**两种。

ViewGroup：ViewGroup控件作为父控件可以更包含多个View控件，并管理其包含的View控件

安卓Activity的界面的架构：Activity--->Window(通常用PhoneWindow实现)--->DecorView(根)--->TitleView/ContentView

DecorView 作为窗口界面的顶层视图，它将要显示的内容呈现在PhoneWindow上，通过WindowManagerService接收View的监听事件
### View的测量
在绘制View之前，安卓都需要对View进行测量，这个过程在onMeasure()中进行

Android为我们提供了一个MeasureSpec类，通过它可以测量View，MeasureSpec是一个32位的int型数据，高2位为测量模式，低30位为测量大小

测量模式有3种
- EXACTLY：精确模式，当我们设置layout_width为具体值的时候，或者match_parent，这种情况使用的就是EXACTLY模式
- AT_MOST：最大值模式，当使用wrap_content时就采用这种最大值模式
- UNSPECIFIED：不指定其大小测量模式，View想多大就多大，通常情况下在绘制自定义View时才会使用

当我们要自定义View的时候，需要重写onMeasure()方法，通过MeasureSpec.getMode()方法获取测量模式，通过MeasureSpec.getSize()的方法获取测量大小。最后返回一个测量值。通过setMeasuredDimension(int x , int y)方法，将测量的值绘制出来
### View的绘制
使用Canvas对象绘制图案，Canvas就相当于一个画板，使用Paint就可以在上面作画了
```
Canvas canvas = new Canvas(bitmap);
//在构造函数中，传入一个bitmap，从此这个bitmap将和canvas绑定
```
### viewGroup的测量
当ViewGroup的大小为wrap_content时，ViewGroup就需要对子View进行遍历，以便获得所有子View的大小，从而确定自己的大小
### 自定义View
在自定义View的时候，我们通常会去重写onDraw()来绘制View的显示内容，如果该View还需要使用wrap_content属性，还需要重写onMeasure()方法。

在View中通常有以下一些比较重要的回调方法
- onFinishInflate():从XML加载组件以后回调
- onSizeChanged():组件大小改变以后回调
- onMeasure():回调该方法来进行测量
- onLayout()：回调该方法来确定显示位置
- onTouchEvent():监听到触摸事件时回调
#### 对现有控件进行拓展
```
Paint p1 = new Paint();
Paint p2 = new Paint();
//初始化Paint画笔
void onDraw(Canvas canvas)
{
    p1.setColor(getResources().getColor(R.color.red));
    p1.setStylr(Paint.FILL);//系统默认为FILL
    p2.setColor(getResources().getColor(R.color.blue));
    p2.setStylr(Paint.FILL);
    canvas.drawRect(0, 0, getMeasureWidth(), getMeasureHeight(), p1);
    //画矩形
    canvas.drawRect(10, 10 , getMeasureWidth()-10, getMeasureHeight()-10, p2);
    //画内圈矩形
    canvas.save();
    canvas.translate(10,0);//把当前画布的原点移到(10,0),后面的操作都以(10,0)作为参照点，默认原点为(0,0)
    super.onDraw(canvas);
    canvas.restore();
  
    //1.save()：用来保存Canvas的状态,save()方法之后的代码，可以调用Canvas的平移、放缩、旋转、裁剪等操作！

    //2.restore()：用来恢复Canvas之前保存的状态,防止save()方法代码之后对Canvas执行的操作，继续对后续的绘制会产生影响，通过该方法可以避免连带的影响！
}
```
**闪动文字特效：**

```
int myViewWidth, mTranslate = 0;;
LinearGradient linearGradient;
Matrix matrix;

@Override
protected void onSizeChanged(int w, int h, int oldw, int oldh) {
    super.onSizeChanged(w, h, oldw, oldh);
    if(myViewWidth == 0){
        myViewWidth = getMeasuredWidth();
        if(myViewWidth > 0){
            Paint paint = getPaint();
            linearGradient = new LinearGradient(0,0,myViewWidth,0,
                    new int[]{Color.BLUE, 0xffffffff, Color.BLUE},
                    null,
                    Shader.TileMode.CLAMP);
            //平铺模式Shader.TileMode.CLAMP：如果着色器超出原始边界范围，会复制边缘颜色
            paint.setShader(linearGradient);
            matrix = new Matrix();
        }
    }
}

@Override
protected void onDraw(Canvas canvas) {
    super.onDraw(canvas);
    if(matrix != null){
        mTranslate += myViewWidth/5;
        if(mTranslate > 2*myViewWidth){
            mTranslate = -myViewWidth;
        }
        matrix.setTranslate(mTranslate,0);
        linearGradient.setLocalMatrix(matrix);
        postInvalidateDelayed(100);//刷新界面
    }
}
```
### 自定义组合控件
1. 在value文件夹中声明属性，新建一个attrs.xml文件
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <declare-styleable name="MyTopBar"> //名字为自己定义组合控件的名字MyTopBar
        <attr name="title" format="string"></attr>
        <attr name="titleSize" format="dimension"></attr>
        <attr name="titleColor" format="color"></attr>
        <attr name="leftText" format="string"></attr>
        <attr name="RightText" format="string"></attr>
        //name为名称，format为属性值
    </declare-styleable>
</resources>
```
2. 创建TypedArray数组存储自定义属性集，并通过这个属性集获取所有的属性
```
public void init(Context context){
    array = context.obtainStyledAttributes(attrs, R.styleable.MyTopBar);
    //第一个参数的attrs需要在MyTopBar(Context context, AttributeSet attrs)这个构造函数中才能有。不然会出现无法获取属性的情况
    //创建TypedArray数组存储自定义属性集
    myTitle = array.getString(R.styleable.MyTopBar_title);
    myleftText = array.getString(R.styleable.MyTopBar_leftText);
    myRigthText = array.getString(R.styleable.MyTopBar_RightText);
    color = array.getColor(R.styleable.MyTopBar_titleColor, 0);
    TitleDimension = array.getDimension(R.styleable.MyTopBar_titleSize, 10);
    //并通过这个属性集获取所有的属性
    array.recycle();
    //使用完以后要释放
}
```
3. 添加需要的控件，将上一步获取的属性为控件设置属性，并为控件设置布局
```
public void com(Context context){
    lbutton = new Button(context);
    rbutton = new Button(context);
    textView = new TextView(context);
//新建控件
    LayoutParams lParams = new LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.MATCH_PARENT);
    lParams.addRule(RelativeLayout.ALIGN_PARENT_LEFT,TRUE);
    addView(lbutton,lParams);

    LayoutParams rParams = new LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.MATCH_PARENT);
    rParams.addRule(RelativeLayout.ALIGN_PARENT_RIGHT, TRUE);
    addView(rbutton, rParams);

    LayoutParams tParams = new LayoutParams(LayoutParams.WRAP_CONTENT, LayoutParams.MATCH_PARENT);
    tParams.addRule(RelativeLayout.CENTER_IN_PARENT, TRUE);
    addView(textView, tParams);
//为控件设置布局
    lbutton.setText(myleftText);
    rbutton.setText(myRigthText);
    textView.setText(myTitle);
    textView.setTextColor(color);
    textView.setTextSize(TitleDimension);
//将上一步获取的属性为控件设置属性
    lbutton.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View v) {
            myListener.leftClick();
        }
    });

    rbutton.setOnClickListener(new OnClickListener() {
        @Override
        public void onClick(View v) {
            myListener.rigthClick();
        }
    });
//设置监听事件
}
```
4. 设置点击事件的回调函数，首先新建一个接口，接口要包括所有的点击事件
```
package com.example.pl.test;

public interface topbarClickListener {
    void leftClick();
    void rigthClick();
}

```
- - -
```
public void setOnTopbarClickListener(topbarClickListener topbarClickListener){
    this.myListener = topbarClickListener;
}
```
5. 引用自定义控件
```
<com.example.pl.test.MyTopBar
    xmlns:app="http://schemas.android.com/apk/res-auto"//添加第一步自定义属性的命名空间
    android:id="@+id/Mytb"
    android:layout_width="match_parent"
    android:layout_height="100dp"
    app:RightText="右"
    app:leftText="左"
    app:title="过小虎"
    app:titleColor="#000000"
    app:titleSize="26sp">
</com.example.pl.test.MyTopBar>
```
### 事件拦截机制分析
什么是事件拦截机制，事件拦截机制就是当用户输入各种事件以后，如何准确的传递给真正需要这个时间的控件。

一个触摸事件对于ViewGroup会产生3个方法，dispatchTouchEvent()、onInterceptTouchEvent()、onTouchEvent();

这三个函数，第一个是分发事件，第二个是截断事件，第三个是完成事件

一个事件的传递过程为，上次的ViewGroup先执行dispatchTouchEvent()，接着是onInterceptTouchEvent()；将事件依次传递下去。当onInterceptTouchEvent()返回值为true时，该控件会截断事件，也就是不在向下传递，由截断事件的控件执行onTouchEvent()完成事件。

一个事件的传递过程是由高向低，即由ViewGroup向View传递。完成过程则相反

对于onTouchEvent()这个函数，当他的返回值为true的时候，将不在向上传递事件完成。即如果View返回了true，上层的ViewGroup就不会执行onTouchEvent()这个函数。

View作为最底层，它没有截断函数onInterceptTouchEvent()。

</font>