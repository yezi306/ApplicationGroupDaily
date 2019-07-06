### 什么是焦点
在非触屏手机时代，我们都是用手机键盘上面的上下左右来选择控件并操作。如今已经是触屏手机了，只要点击就可以获取相应的焦点并控制控件。==所以焦点的意思就是：标记目前选中的位置==

### 获取焦点的前提
所有的控件只有在设置了clickable = "true"之后才可以获取焦点，毕竟如果都不能点击，谈何获取焦点的事

### focusable：
当focusable属性的值为true的时候，表名该控件可以通过一定的操作（点击等）将焦点转移到当前控件。如果为false，说明无法将焦点转移至此控件

简单的说：==focusable决定一个控件能否被选中（获得焦点）==

### focusableInTouchMode：
在默认情况下，点击一个按钮时可以触发它的点击事件，但是却无法使控件处于焦点状态。这个时候可以将focusableInTouchMode设置为true，这样可以当我们点击一个控件的时候，首先会将焦点移到改控件，随后在点击，才可以触发按钮的点击事件

==注意：focusableInTouchMode设置为true以后该控件会自动优先获取焦点==

### 应用：
当我们使用EditText的时候，系统会默认让EditText优先获取焦点，所以当我们打开含有EditText的活动时会自动弹出软键盘，那么我们要怎么取消这种自动打开软键盘呢？

我们可以在EditText的根布局上，为它的==根布局==设置focusableInTouchMode属性为true，设置focusable为true，这样我们新进入一个活动的时候根布局会比EditText更优先获取焦点

### 拓展知识：----如何手动打开或关闭软键盘

#### 打开：
```
InputMethodManager im = (InputMethodManager) context.getSystemService(Context.INPUT_METHOD_SERVICE);
im.showSoftInput(View, flags);//第一个参数为需要输入的View一般为EditText。第二个参数为一个标志，无特殊要求输入0即可
```
#### 关闭：
```
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
imm.hideSoftInputFromWindow(view.getWindowToken(), flag);//第一个参数传入一个IBinder，这里通过View获取即可，第二个参数为一个标志，无特殊要求输入0即可
```
#### 切换开关状态----软键盘关闭则打开，打开则关闭
```
InputMethodManager imm = (InputMethodManager) getSystemService(Context.INPUT_METHOD_SERVICE);
imm.toggleSoftInput(0, InputMethodManager.HIDE_NOT_ALWAYS);
```
