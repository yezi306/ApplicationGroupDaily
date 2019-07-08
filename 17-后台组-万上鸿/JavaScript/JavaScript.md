[toc]
# 1 JavaScript了解
## 1.1 JavaScript是什么？
JavaScript是一种小型的、轻量级的、面向对象的、跨平台的客户端脚本语言。<br/>
JavaScript是嵌入到浏览器当中的去的，只要你的电脑有浏览器就可以执行JS程序了。<br/>
JavaScript是一种面向对象的程序语言。<br/>
在程序中，对象是由“属性”和“方法”构成。<br/>
在现实中，男女朋友就是一个“对象”。“东西”就是“对象”。一个“物体”就是“对象”.

注意：JS中的对象只要会用就可以了，不需要我们自己去开发对象。

跨平台：JS程序可以在多种平台下运行，如：windows,linux,mac,IOS等<br/>

客户端脚本程序：JS只能在客户端的浏览器来运行，不能在服务器端来运行。

浏览器是一个翻译器，可以翻译三种代码：HTML代码、CSS代码、JavaScript代码。
## 1.2 JavaScript能干什么？
1. 表单验证：是JS最基本的功能。
2. 动态HTML:可以实现一些动态的、重复的效果。
3. 交互式：人机交互，通过键盘或鼠标，与网页中的元素进行交互。
## 1.3 JavaScript名称的由来？
JavaScript最初叫“LiveScript”,是网景公司(Netscape)公司开发，为自己的浏览器Navigator2.0开的客户端语言。想借助Java的名气很快成长起来，因此改名为JavaScript。<br/>
Java和JavaScript是两个公司的两个东西。

# 2 JavaScript基本知识
## 2.1 <script></script>标记
JS代码也是嵌入到HTML文档中去。<br/>
同一个网页中，可以有HTML代码、CSS代码、JavaScript代码。
通过<script></script>来引入JS程序代码
```
<script>
    //在<body>中输出一句话
    document.write("我是被踢出来的！");
</script>
```
## 2.2 常用的两个客户端输出方法
document.write(str)
1. 描述：在网页的<body>标记，输出str的内容。
2. document意思“文档”，就是整个网页了。
3. document是一个文档对象，代表整个网页。
4. write()是document对象的一个输出方法。
5. “.”小数点：通过小数点(.)来调用对象的方法。
6. str：表示要输出的内容。

window.alert(str)
1. 描述：在当前窗口中弹出一个警告对话框，str为对话框中显示的内容。
2. window代表当前浏览窗口，window是一个窗口对象。
3. alert()方法：弹出一个对话框。
4. str：表示要输出的内容。
```
window.alert("你看见我的吗？我在呢？")
```
## 2.3 JavaScript中的注释
`//或/* 多行注释*/`

# 3 变量
## 3.1 变量的声明
语法：`var 变量名=变量值`

例
```
var name;
var name,sex,edu;
var name="张三";
```

字符型：var a="10";
整数型：var b=a+10;

单引号内只能嵌套双引号；
双引号只能嵌套单引号

弹窗中的换行，只能使用\n实现；而不能使用`<br>`,只能`<body>`中的`<br>`才能解析成换行符

## 3.2 布尔型
```
var a=true;
var b=false;
```
## 3.3 未定义型
未赋值是，将返回为定义性，未定义型的值只有一个undefined'
```
var a;
document.write(a);
```
## 3.4 空值
当一个对象不存在时，将返回空值只有一个null.

也可以理解为：是一个对象的占位符。

如果你想清除一个变量的话，可以给赋值一个null的值。
```
var a=100;
var a=null;
```
# 4 语句
## 4.1 if条件判断
1. 语法结构——只判断true，不判断false
```
if(条件判断：结果只有两个true或false)
{
    条件为true，将执行该代码；
}else{
    
}
```
if和else必须小写

# BoM和DOM简介
