[toc]

<font size = "4">

### 滑动效果是如何产生的
滑动一个View就是移动一个View，想要实现View的滑动，就==必须监听用户的触摸事件==，并根据事件传入的坐标，动态的改变View
#### Android坐标系
在Android中，屏幕最左上角的顶点作为Android的坐标原点，从这个点**向右**是X轴正方向，**向下**是Y轴正方向

==系统提供了==

> getLocationOnScreen(intlocation[])    
//用于获取Android坐标系中点的位置（即左上角在Android在坐标系中的坐标）

在触控事件中也可以使用
> getRawX()、getRawY()获取Android在坐标系中的坐标

#### 视图坐标系

同Android坐标系不同的是，视图坐标系的原点是以父视图左上角为坐标原点

在触控事件中可以使用
> getX()、getY()获取试图坐标系中的坐标

#### 触控事件----MotionEvent
通常情况下我们会在onTouchEvent(MotionEvent event)方法中通过event.getAction()方法来获取触控事件，并通过switch-case方法来筛选

下面总结了一些API，结合Android坐标系来看看该如何使用他们

==**View提供的获取坐标方法**==
1. getTop():获取被触摸View自身的==顶边==到其父布局的==顶边==的距离
2. getLeft():获取被触摸View自身的==左边==到其父布局的==左边==的距离
3. getRight():获取被触摸View自身的==右边==到其父布局的==左边==的距离
4. getButton():获取被触摸View自身的==低边==到其父布局的==顶边==的距离

==**MotionEvent提供的获取坐标方法**==
1. getX():获取点击事件距离==控件左边==的距离（视图坐标）
2. gety():获取点击事件距离==控件顶边==的距离（视图坐标）
3. getRawX():获取点击事件距离==整个屏幕左边==的距离（绝对坐标）
4. getRawY():获取点击事件距离==整个屏幕顶边==的距离（绝对坐标）

### 实现滑动的7种方法
实现滑动的基本思想：

当触摸View时，系统记下当前触摸点坐标；当手指移开时，系统记下移动后的触摸点坐标，从而获得到相对于前一次坐标点的**偏移量**，并通过偏移量来修改View的坐标，这样不断重复，从而实现滑动的过程。

#### layout方法
1. 在回调onTouchEvent的时候记录初始坐标
2. 在ACTION_DOWN事件中记录触摸点的坐标
3. 在ACTION_MOVE事件中计算偏移量
```
public boolean onTouchEvent(MotionEvent event){
    int lastX, lastY;
    int x = (int)event.getX();
    int y = (int)event.getY();
    switch(event.getAction()){
        case MotionEvent.ACTION_DOWN:
            lastX = x;
            lastY = y;
            break;
        case MotionEvent.ACTION_MOVE:
            int offsetX = x - lastX;
            int offsetY = y - lastY;
            layout(getLeft()+offsetX, getTop()+offsetY, getRight()+offsetX, getButtom()+offsetY);
            //如果使用Android坐标系来计算的时候需要将lastX,lastY重新设置初始坐标。
            break;
    }
}
```
#### offsetLeftAndright()和offsetTopAndBottom()
这个方法是系统提供用于左右、上下移动的API，将计算出来的偏移量传入即可达到效果
```
offsetLeftAndRight(offsetX);
offsetTopAndBottom(offsetY);
```

#### LayoutParams
1. 使用getLayoutParams()获取Params
2. 通过setLayoutParams()设置布局

#### scrollTo和scrollBy
scrollTo表示移动到一个具体的坐标点(x, y),而scrollBy(dx, dy)表示移动的增量

==注意：这两个方法是移动触摸点的父布局的内容，所以在使用的时候要用getParent.scrollTo，这样才能移动自己。并且它的参照物是触摸点本身，所以移动的增量其实等价于移动父布局，所以参数要传入相反的值==

#### Scroller
1. 初始化Scroller，通过构造函数new Scroller(context);
2. 重写computeScroll()方法，实现模拟滑动
```
//模板

public void computeScroll(){
    super.computeScroll();
    if(mScroller.computeScrollOffset()){
        ((View)(getPatent)).scrollTo(mScroller.getCurrX(), mScroller.getCurrT());
        invalidate();
        //重绘View
    }
}
```
3. startScroll开启滑动模拟
```
mScroller.startScroll(viewParent.getScrollX(), viewParent.getScrollY(), x, y, dution);
//x， y为偏移量，dution为持续时间
```

</font>