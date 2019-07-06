### 常见控件的使用方法
控件的属性：可见(visible默认)、不可见(invisible)、gone.

可见：就是控件可以看见。

不可见：控件不可以看见，但是会占用屏幕空间

gone：控件不可见，且不会占用屏幕控件。

**可以通过setVisbility()的方法设置控件属性**。

**可以通过getVisbility()的方法获取控件属性**。
#### TextView
设置id，宽度，高度，文字，颜色，字体大小就不说了

gravity:用来设置字体对齐方式。有center、top、bottom等方式。**可以用“|”指定多个值**

#### Button
由于系统会对Button中的所有英文字母进行大写转换，如果你不想要这样的效果,更改就可以了
```
android:textAllCaps="false"
```
去除Button自带的阴影效果
```
style="?android:attr/borderlessButtonStyle"
```
就是一个按钮
```
<selector xmlns:android="http://schemas.android.com/apk/res/android">
    <item android:state_pressed="true">
        <shape>
            <stroke
                android:color="#000">

            </stroke>
        </shape>
    </item>
    <item android:state_pressed="false">
        <shape>
            <solid
                android:color="#d3d3d3">
            </solid>
        </shape>
    </item>
</selector>
```
设置点击事件（通过接口的方式设置）
```
public class Main extends AppCompatActivity implements View.OnClickListener{
    onCreate(){
        button.setOnClickListener(this);
    }
    
    public void onClick (View v){
        switch(v.getId()){
            case R.id.button:
                ....
                break;
        }
    }
}
```
==onClick(View v)函数，这个函数唯一的参数是一个View，它表示来自夫层的ContentView，所以可以通过"v.*"改变夫层View的状态和属性。==

自定义按钮形状
#### EditText
可以给用户输入东西的文本框。
如登陆界面的账号密码输入框框。

- hint:可以书写提示性文字。这些文字当我们输入的时候会自动消失。
- maxLines: 可以指定输入不多于多少行。当超过这个长度的时候，文字就会向上滚。不会超过两行的大小。
- getText():这是在main界面可以写的函数获取EditText输入的东西。
- inputType:可以指定用户输入的是什么信息。其中textPassword选项会让用户输入的变成像密码一样，输一个就变成*号。
- ![image](http://wx1.sinaimg.cn/mw690/0060lm7Tly1fv71ggzadpj30or0cpgmd.jpg)
- **进入活动以后默认打开键盘的方法**
```
在活动的配置文件中加入
<activity android:name=".Ss"
    android:windowSoftInputMode="stateVisible|adjustResize">

</activity>
```
#### ImageView
展示图片的控件
- src:可以添加文件，但是记得把图片拉到drawable文件夹下。
- setImageResource(图片)：在活动代码区可以用这个改变图片。
- scaleType：可以选择图片的填充情况

(**fitXY**：不管图片拉伸直接填满框框)

(**fitCenter**:将图片等比例缩小，直到可以全部显示出来)

(**centerCrop**:等比例放大，直到沾满整个框框)
#### progressBar
用于在界面上显示一个进度条， getProgress() 获取进度值

可以通过style来更换样式，例如圆形和条形

还可以通过max = 来设置进度条的最大值

```
style="?android:attr/progressBarStyleHorizontal"
android:max="100"
```
#### AlertDialog
这个可以弹出一个对话框，对话框是置顶于所有的界面元素之上的，可以屏蔽掉其他控件的交互能力**一般用于警告用户**
```
AlertDialog.Builder dialog = new AlertDialog.Builder(MainActivity.this);
dialog.setTitle("XXX");
dialog.setMessage("AAAA");
dialog.setCancelable(false);
dialog.setPositiveButton("OK", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialogInterface, int i) {
    }
});
dialog.setNegativeButton("Cancel", new DialogInterface.OnClickListener() {
    @Override
    public void onClick(DialogInterface dialogInterface, int i) {
        
    }
});
dialog.show();
```
首先通过Builer创建一个实例，然后为这个对话框设置标题、内容、可否被访问等属性，然后设置两个按钮并设置这两个按钮的事件。

#### ProgressDialog
和上面的一样，也是弹出一个对话框，但是这个会加一个进度条，**用于提示用户这个活动比较慢，耐心等待**

它的使用和上一个也是十分相似的，首先创建实例。progressDialog x  =new progressDialog(Main.this);

这里需要注意的是，**setCancelable**如果是false代表不可以通过back键来关闭的，所以必须要在代码中控制好，在加载完数据以后使用dismiss()来关闭对话框
### RadioButton
勾选选项
```
android:drawableTop="@drawable/radio1"
//在选项上添加图片，可以通过新建xml设置选中与未选中的不同图片

android:button="@null"
//将框框隐藏掉

android:textColor="@color/textcolor"
//设置选项文字，通过建立color.xml文件设置选中与未选中的事件
```
### CheckBox
多项选择框

**RadioButton和CheckBox的区别：**

1.单个RadioButton在选中后，通过点击无法变为未选中

单个CheckBox在选中后，通过点击可以变为未选中
2. 一组RadioButton，只能同时选中一个

一组CheckBox，能同时选中多个
3. RadioButton在大部分UI框架中默认都以圆形表示

CheckBox在大部分UI框架中默认都以矩形表示
### ListView
我们的手机联系人，可以向下向上滑动查看里面的联系人。这样的功能就是ListView

ListView是用来存放多数据的一个框框，所以我们**首先**就要准备好数据。然后我们要将数据传递给ListView，传递数据需要适配器，ArrayAdapter就是一个用来传递数据的适配器。
```
ArrayAdapter<T泛型> x = new ArrayAdapter<>("传入当前上下文", "ListView的子项ID", "数据");
```
再将配置好的适配器传递给ListView。

listView.setAdapter(x);

当数据都是文本的时候，我们可以用android.R.layout.simple_list_item_i作为第二个参数即子项布局的id。
#### 自定义ListView
当我们的数据不是简单的文字，比如我们的ListView的每个是图片加文字的时候，我们就需要自己定义一个数据Listview

和之前的步骤一样，首先我们要定义出数据来，既然数据不是简单的文字。我们就要创建一个类。比如一个图片和一段文字。

在类定义好以后我们就需要画出布局，

画出布局以后就要自己写一个适配器了，继承ArrayAdapter,他的构造器和普通的适配器一样需要三个参数。一个是当前文本的内容，第二个是资源，第三个是数据

最重要的就是getView函数的重写。我们每当一个子项被滚动到屏幕内的时候就会调用这个函数

首先获得当前实例getItem

LayoutInflater.from(getContext()).inflate(resourceId,null);为子项加载我们传入的布局

**简单来说适配器就是要传一个主面板，一个图案，图案的数据**
#### ListView的运行效率
第一种一般般的优化方法：

我们重写getView的时候第二个参数是View ConverView。这个参数就是用来将之前加载好的布局进行缓存。以便之后的使用。这样就不用不断的重画界面，造成卡顿。

第二种方法:

新建一个内部类存放控件的实例。对控件的实例进行缓存。
```
public class ListTest extends ArrayAdapter {
    private int resourceId;
    public ListTest(Context context, int textRecoureId, List<Fruit> fruitList){
        super(context, textRecoureId, fruitList);
        resourceId = textRecoureId;
    }
    @NonNull
    @Override
    public View getView(int position, @Nullable View convertView, @NonNull ViewGroup parent) {
        Fruit fruit = (Fruit) getItem(position);
        View view = null;
        ViewHolder viewHolder;
        if(convertView == null){
            view = LayoutInflater.from(getContext()).inflate(resourceId, null);
            viewHolder = new ViewHolder();
            viewHolder.imageView = view.findViewById(R.id.I_1);
            viewHolder.textView = view.findViewById(R.id.Te_2);
            view.setTag(viewHolder);
        }else{
            view = convertView;
            viewHolder = (ViewHolder)view.getTag();
        }
        viewHolder.imageView.setImageResource(fruit.getImageID());
        viewHolder.textView.setText(fruit.getName());
        return view;
    }
    class ViewHolder{
        ImageView imageView;
        TextView textView;
    }
}
```
### ScrollView(垂直)、HorizontalScrollView(水平)
用于设置滚动条
```
 <ScrollView
    android:layout_width="fill_parent"
    android:layout_height="wrap_content" >
    <TextView
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"
        android:text="@string/hello"
        android:textSize="90sp" />
    <TextView>
<ScrollView>
```
这样如果TextView如果一个屏幕显示不完的时候，可以有滚动条查阅
### 圆形图片CircleImageView
建立依靠
```
compile'de.hdodenhof:circleimageview:2.2.0'
```
### RecyclerView
建立依靠
```
compile 'com.android.support:recyclerview-v7:28.+'
```
准备适配器
```
class Myadapt extends RecyclerView.Adapter<Myadapt.ViewHolder>{
    private List<> list;
    static class ViewHolder extends RecyclerView.ViewHolder{
        ImageView x;
        TextView y;
        ViewHolder(View view){
            x = view.findViewById(R.id.xx);
            y = view.findViewById(R.id.yy);
        }
    }
    
    public Myadapt(List<> list){
        this.list = list;
    }
    
    @Override       //第二个参数代表一个View，表示当前布局的种类
    public ViewHolder onCreateViewHolder(ViewGroup parent, int viewType){
        View view = LayoutInflater.from(parent.getContext()).inflate(R.layout.布局文件, parent, false);
        ViewHolder holder = new ViewHolder(view);
        return holder;
    }
    
    @Override
    public void onBindViewHolder(ViewHolder holder, int position){
        Fruit fruit = list.get(position);
        holder.fruitImage.setImageResource(fruit.getImafeId());
    }
    @Override
    public void getItemCount{
        return list.size();
    }
}
```
主活动调用适配器
```
RecyclerView recyclerview = findViewById(R.id.xx);
LinearLayoutManager layoutManager = new LinearLayoutManager(this);
recyclerview.setLayoutManager(layoutManager);
Myadapt adaptr = new Myadapt(list);
recyclerview.setAdapter(adaptr);
```
如果需要把list变成横向的
```
layoutManager.setOrientation(LinearLayoutManager.HORIZONTAL);
```
瀑布效果
```
StaggeredGridLayoutManager layoutManager = new StaggeredGridLayoutManager(3, StaggeredGridLayoutManager.VEWTICAL);
//第一个参数是要排几列，第二个参数是需要垂直还是水平排
```