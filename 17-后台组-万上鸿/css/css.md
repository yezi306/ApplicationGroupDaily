[toc]

# 1.CSS简介
CSS（Cascading Style Sheets)层叠样式表

CSS的主要目的：给HTML标签添加各种各样的表现（格式、样式）比如：文字样式、背景、文本样式、链接样式。

提示：CSS是给HTML标记加的样式；JS是给HTML标记加的行为。HTML标记是最先出现的

1. HTML超文本标注语言：各种HTML标记
2. CSS层叠样式表：给HTML标记加的样式表
3. JavaScript脚本程序：给HTML标记加的程序

# 2.CSS语法格式
```
         属性   值           属性    值
  h1    {color:red;       font-size:14px;}
选择器     声明                 声明

```

1. 一个CSS规则，由“选择器”和“格式声明语句”构成。
2. “选择器”：就是选择HTML标记，换句话说：就是给哪个HTML标记加样式。
3. “格式声明语句”：由{}构成，{}中是各种格式的语句
4. 一条格式语句，由“属性名：属性”构成。
5. 每一条格式语句，必须用英文下的分号“；”结束。
6. 属性名，就是CSS中的各种属性，这些属性名都是固定的。
7. 属性值，一个属性名可以取不同的值，这个值不加引号。
8. CSS中的数字单位都是px，这个px不能省略。

## 2.1 选择器
### 2.1.1基本选择器
#### 2.1.1.1 "*"选择器<br/>
描述：将匹配所有的HTNL标记，只要<body>中存在的标记都会改变的<br/>
语法：*{color:red;}<br/>
注意：“*”尽量少用，因为IE6不支持。
```
*{
    color:red;    /* 所有的HTML标记的颜色都会变成红色 */
}
```
#### 2.1.1.2 标记选择器<br/>
描述: 将匹配指定的HTML标记<br/>
语法：h1{color:red;}<br/>
注意：CSS标签选择器，与HTML标记的名称一样，但不能加尖括号。<br/>
```
p{
    /* 网页中所有的<p>标记的“一类”是：每个HTML标记都有一个class属性 */
}
```
#### 2.1.1.3 class选择器(类选择器)<br/>
描述：给一类HTML标记加样式。这里所指的“一类”是：每个HTML标记都有一个class属性，且class的值一样。class属性是公共属性，每个HTML标记都有

类选择器的名称，必须以“.”开头，后跟HTML标记的class属性的值

==注意：HTML标记的class属性的值，不能以数字开头==
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .myClass{
            color: red;
            background-color: yellow;
        }
    </style>
</head>
<body>
    <p class="myClass">hi噢近日苹果鸡皮未激活批文件很平静颇为惊魂破</p>
    <p class="myClass">hoijokppfbejkk[osjipv[owiejpbo[ktwo[bjwto[jbo</p>
</body>
</html>
```
#### 2.1.1.4 id选择器<br/>
描述：给指定id的元素添加样式。<br/>

注意：网页HTML标记的id属性的值，必须是唯一的

每一个HTML标记都有一个id的公共属性

注意：id属性一般给JS使用的，不是让你来加样式。class属性只能给CSS用，不能给JS使用

id选择器的名称，必须以“#”开头，后跟HTML标记的id属性的值。
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        #myId{
            color: red;
            background-color: blue;
        }
    </style>
</head>
<body>
    <p id="myId">gyhjkopoiuytfyuoiiuygujokpiugjkhvhjjojvhhiojjhvj</p>
</body>
</html>
```
### 2.1.2 组合选择器
#### 2.1.2.1 多元素选择器
描述：给多个元素加同一样式,多个选择器之间用逗号“，”隔开。

例1: （h1,h2）
```
h1,p,div,body{
    color：red;
}
```

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        h1,h2{
            color: red;
            background-color: blue;
        }
    </style>
</head>
<body>
    <h1>景点</h1>
    <h2>背景</h2>
</body>
</html>
```
例2  （.title）和h1
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .title,h1{
            color: red;
            background-color: blue;
        }
    </style>
</head>
<body>
    <h1 class="title">景点</h1>
    <h1>背景</h1>
</body>
</html>
```
例3 （div.title）和
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div.title,h1{
            color: red;
            background-color: blue;
        }
    </style>
</head>
<body>
    <h1 class="title">景点</h1>
    <h1>背景</h1>
    <div class="title">景点</div>
</body>
</html>
```
#### 2.1.2.2 后代元素选择器
描述：给某个标签的某一个后代元素加样式。选择器之间用“空格”隔开

举例：div .title{color:red;}
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div h1.title{
            background-color: blanchedalmond;
        }
        div p.title{
            background-color: tomato;
        }
    </style>
</head>
<body>
    <div>
        <h1 class="title">八达岭</h1>
        <p class="title">风景很漂亮</p>
    </div>
</body>
</html>
```
#### 2.1.2.3 子元素选择器
描述：给某个元素的子元素添加样式

举例：.box>h1.title{color:red;}
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        /* 查找div的子元素h1,而不查找孙子元素h1 */
        .box>h1.title{
            color: red;
            background-color: blue;
        }
    </style>

</head>
<body>
    <div class="box">
        <h1 class="title">天安门广场</h1>
        <div >
            <h1 class="title">通道</h1>
        </div>
    </div>
</body>
</html>
```
## 2.2 CSS注释
CSS注释：
` /* CSS注释内容 */ `
HTML注释：
` <!- HTML注释 -> `

## 2.3 尺寸属性
width:元素宽度，一定要加px单位。<br/>
height：元素高度。

## 2.4 CSS字体属性
font-size:文字大小。如:font-size:14px;<br/>
font-family:字体。如：font-family:微软雅黑;<br/>
font-style:斜体，取值：italic。如：font-style:italic<br/>
font-weight:粗体,取值：bold。如：font-weight:bold;<br/>

## 2.5 CSS文本属性
color：文本颜色<br/>
text-decoration:文本修饰线，取值：none(无)、underline(下划线)、overline(上划线)、line-throught(删除线)<br/>
text-alight：文本水平对齐方式，取值：left、center、right<br/>
line-height：行高，可以用固定值，也可以用百分比。如：；line-height:24px;line-height:150%;<br/>
text-indext:首行缩进。如：text-index:28px;<br/>
letter-spacing:字间距。<br/>
padding:内填充（同时给四个边添加距离，即文字到边框的距离）

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 1000px;
            border: 1px solid #444;
            margin: 0px auto;/* div在网页中居中，Firefox支持 */
            padding:20px;
        }
    </style>
</head>
<body>
    <div class="box">
        <h1>中国</h1>
        <p>中国共产党万岁</p>
    </div>
</body>
</html>
```
例2
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="utf-8">
    <title></title>
    <style>
        .box{
            width: 1000px;
            border: 1px solid #444;
            margin: 0px auto;/* div在网页中居中，Firefox支持 */
        }
        .box{
            font-family: 楷体;
            color: #003399;
            font-size: 14px;
            text-indent: 28px;/* 首行缩进 */
            line-height: 180%;/* 行高 */
        }
        .box .p1  span.span1{
            color: #ff00ff;
            font-size: 36px; 
            font-family: 黑体; /* 字体类型 */
        }
        .box .p1 span.span2{
            color: #ffff33;/* 昨天颜色 */
            font-size: 26px;/* 字体大小 */
            font-style: italic;/* 斜体 */
        }
        .box .p2{
            font-weight: bold;/* 加粗 */
            text-decoration: underline;/* 下划线 */
            letter-spacing: 10px;/* 字间距 */
        }
    </style>
</head>
<body>
    <div class="box">
        <h1>中国</h1>
        <p class="p1">中国<span class="span1">共产党</span><span class="span2">万岁</span></p>
        <p class="p2">不忘初心跟党走</p>
    </div>
</body>
</html>
```
## 2.6 CSS伪类选择器：给超链接加的样式(链接的不同状态加样式)
一个超链接，有四个状态：
1. 正常状态(:link)：鼠标没有放上之前链接的样式。
2. 放上状态(:hover)：鼠标放到链接上时的、样式。
3. 激活状态(:action)：按住鼠标左键不松开的样式，这个状态特别短暂。
4. 访问过后的状态(:visited)：按下鼠标左键，并弹起，这时的样式效果

在平时工作中，会使用一下写法，来给链接加不同的样式

` a:link a:visited{color: red;text-decoration: none;} //通常将"正常状态"和“访问过的状态”合二为一 `

` a:hover{color:#990000;text-decoration:underline;}`

例
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div{
            width: 600px;
            border: 1px solid #333;
            padding: 20px;/* 同时给四个边加10px的内填充 */
        }
        .box a:link,.box a:visited{
            color: #003399;
            text-decoration: none;
        }
        .box a:hover{
            color: #FF0000;
            text-decoration: underline;
        }

        /* a.a1     给class=a1的<a>元素添加样式
           a.a1:link //给class=a1的<a>元素的正常状态，添加样式
         */
        .box a.a1:link,.box a.a1:visited{
            color: #00cc00;
            font-size: 24px;
            background-color: #ffff33;
        }
        .box a.a1:hover{
            color: red;
            text-decoration: underline;
        }
    </style>
</head>
<body>
    <div class="box">
        <a href="#">网站首页</a>
        <a href="#">公司简介</a>
        <a href="#" class="a1">新闻动态</a>
        <a href="#">产品中心</a>
        <a href="#" class="a1">最新发布</a>
    </div>
</body>
</html>

```
## 2.7 CSS列表属性 
List-style:列表样式，取值：none。去掉项目符号或编号前面的各种符号。<br/>
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        u1,li{
            list-style: none;//去除符号
        }
    </style>
</head>
<body>
    <ul>
        <li>北京市</li>
        <li>天津市</li>
        <li>上海市</li>
        <li>北京市</li>
        <li>北京市</li>
    </ul>
</body>
</html>
```
## 2.8 边框属性、内边框、外边框
### 2.8.1 边框属性：每个元素都可以加边框线
border-left:左边框线
1. 格式：border-left:粗细   线型    线的颜色
2. 线型：none(无线)、soild(实线)、dashed(虚线)、dotted(点状线)
3. 举例：`border-left：5px dashed red;`

border-right:右边边框线。


border-right：右边框线。

border-bottom：下边框线。

border：同时给四个边加边框线。

例
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        div.news{
            width: 500px;
            height:400px;
            background-color: #f0f0f0;
            border-left: 5px solid red;
            border-right: 5px dashed green;
            border-bottom: 5px dotted blue;
        }
        /* 表单中的各元素，都是行内元素
         表单中的各元素，可以指定width或height
         我们更改文本框的宽度和高度。
         */
        input{
            width: 400px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <input type="text" value="成绩" />
    <div class="news"></div>
</body>
</html>
```
### 2.8.2 CSS内边框属性：边框线到内容间的距离

==注意：平常我们所说的width和height属性，它们指内容的宽度和高度，不含内、外边距、边框线。==

Padding-left：左填充距离，左边线到内容间的距离

Padding-right：右填充距离，右边线到内容间的距离

Padding-top：上填充距离，上边线到内容间的距离

Padding-button：下填充距离，下边线到内容间的距离

缩写方式
1. padding：10px;    //四个边的内填充分别为10px
2. paddinh:10px 20px;//上下为10px，左右为20px
3. padding：5px 10px 20px;//上为5px，左右为10px，下为20px
4. padding：5px 10px 15px 20px;//顺序为“上右下左” 上为5px，右为10px 下为10px，左为20px

例
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 400px;
            background-color: #ccc;
            border: 1px solid #444;
            padding: 20px;
        }
    </style>
</head>
<body>
    <p class="box">
        惠州学院（Huizhou University）是广东省省属公办综合性
        普通本科院校，是广东省与惠州市共建高校，位于全国文明城市惠州。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务...
    </p>
</body>
</html>
```
### 2.8.3 CSS外边距属性：边线往外的距离（通常不用，兼容性问题）
Margin-left: 左边线往外的距离。

Margin-right：右边线往外的距离。

Margin-top：上边线往外的距离。

Margin-bottom：下边线往外的距离。

缩写方式
1. margin：10px;    //四个外边距分别为10px
2. margin:10px 20px;//上下外边距10px，左右外边距20px
3. margin：5px 10px 20px;//上外边距5px，左右外边距10px，下外边距20px
4. margin：5px 10px 15px 20px;//顺序为“上右下左” 上外边距5px，右外边距10px 下外边距10px，左外边距20px

例：
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 400px;
            background-color: #ccc;
            border: 1px solid #444;
            padding: 20px;/* 内填充：边线往里的距离 */
            margin: 20px;/* 外边距：边线往外的距离 */
            float: left;/* 浮动：让多个块元素并列显示 */
        }
    </style>
</head>
<body>
    <p class="box">
        惠州学院（Huizhou University）是广东省省属公办综合性
        普通本科院校，是广东省与惠州市共建高校，位于全国文明城市惠州。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务...
    </p>
    <p class="box">
        惠州学院（Huizhou University）是广东省省属公办综合性
        普通本科院校，是广东省与惠州市共建高校，位于全国文明城市惠州。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务...
    </p>
    <p class="box">
        惠州学院（Huizhou University）是广东省省属公办综合性
        普通本科院校，是广东省与惠州市共建高校，位于全国文明城市惠州。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务...
    </p>
</body>
</html>
```
### Firefox浏览器中，Firebug试调工具的安装使用
如果你的Firefox的版本高于30的话，请使用Firebug2.0及以上版本。

如果你的Firefox的版本低于30的话，请使用Firebug1.9、Firebug1.7


### 实战
实战1：
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        /* 全局样式设置 */
        body,ul,li,h4,a{
            margin: 0px;
            padding: 0px;
        }
        ul,li{
            list-style: none;
        }
        body{
            font-size: 12px;
            background-color: #ccc;
            font-family: 宋体;
        }
        a:link,a:visited{
            color: #003366;
            text-decoration: none;
        }
        a:hover{
            color: red;
        }
        /* 开班信息模块 */
        .kaiban{
            width: 295px;
            border: 1px solid red;
            background-color: #fff;
            margin:50px auto;/* div元素在网页中居中对齐（Firefox）*/
        }
        .kaiban .title{
            height: 35px;
            line-height: 35px;
            color: #ffffff;
            font-size: 16px;
            padding-left: 40px;
            background-image: url("images/03.jpg");
        }
        .kaiban .content{
            padding: 5px 10px;
        }
        .kaiban .content h4{
            padding: 5px 0px;
        }
        .kaiban .content li{
            border-bottom: 1px dashed #ccc;
            padding: 3px 0px;
        }
        .kaiban .content span{
            font-weight: bold;
            float: right;/* 右浮动 */
        }
        .red{
            color: red;
        }
        .blue{
            color: blue;
        }
    </style>
</head>
<body>
    <div class="kaiban">
        <div class="title">PHP培训开班信息</div>
        <div class="content">
            <h4>PHP基础班</h4>
            <ul>
            <li><a href="#">北京--第39期（2015年07月09日）</a><span class="red">预约报名</span></li>
            <li><a href="#">北京--第38期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            <li><a href="#">北京--第37期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            </ul>
            <h4>PHP就业班</h4>
            <ul>
            <li><a href="#">北京--第39期（2015年07月09日）</a><span class="red">预约报名</span></li>
            <li><a href="#">北京--第38期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            <li><a href="#">北京--第37期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            </ul>
            <h4>PHP远程班</h4>
            <ul>
            <li><a href="#">北京--第39期（2015年07月09日）</a><span class="red">预约报名</span></li>
            <li><a href="#">北京--第38期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            <li><a href="#">北京--第37期（2015年07月09日）</a><span class="blue">爆满已开班</span></li>
            </ul>
        </div>
    </div>
</body>
</html>
```

## 2.9 CSS背景属性
background-color：背景颜色

background-image：背景图片地址。如：background-image:url(images/bg.gif)

background-repeat；背景平铺方式。取值：no-repeat(不平衡)、repeat-x(水平方向)、repeat-y(垂直方向)

background-positon: 背景定位。格式：background-position:水平方向定位 垂直方向定位；  
1. 用英文单词定位：background-position:left/center/right  top/center/bottom
2. 用固定值固定：background-position：50px 50px.//背景距离容器的左边50px，容器顶端50px
3. 用百分比定位：50% 50%;//水平居中，垂直居中
4. 用混合定位：background-position:left 10px;//背景靠左对齐，距离容器顶端10px

简写方式
1. background：背景色 背景图 平铺方式 定位方式;
2. 举例：background：url(images/bg.gif) no-repeat center center;
3. 举例：background：#ccc url(images/bg.gif) no-repeat center center;

例
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        /* 全局CSS设置 */
        body,h1,p{
            margin: 0;
            padding: 0;
        }
        ul,li,ol{
            list-style: none;
        }
        a:link,a:visited{
            color: blue;
            text-decoration: none;
        }
        a:hover{
            color: red;
        }
        body{
            font-size: 14px;
            color: #444;
            font-family: 宋体;
            background-color: #ccc;
        }
        /* 新闻模块 */
        .news{
            width: 600px;
            margin: 40px auto;/* div元素在网页中居中显示 */
            background-color: #444;
            padding: 20px 20px 130px;
            background: #fff url("images/07.jpg") no-repeat 690px bottom;
        }
        .news h1{
            text-align: center;/* 文本居中 */
            padding: 10px 0px;
        }
        .news p{
            text-indent: 28px;/* 首行缩进 */
            line-height: 150%;/* 行间距，原来行高的1.5倍 */
            padding: 14px 0px;
        }
    </style>
</head>
<body>
    <div class="news">
        <h1>
            惠州学院（Huizhou University）
        </h1>
        <p>
            惠州学院（Huizhou University）是广东省省属公办综合性普通本科院校，是广东省与惠州市共建高校，
            位于全国文明城市惠州。
        </p>
        <p>
            惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，后改办为“广东省立惠州师范学校”。
            1978年12月，经国务院批准升格为专科院校，更名为“惠阳师范专科学校”。
            1993年9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育学院、西北纺织学院惠州分院联
            合办学基础上，成立专科层次的“惠州大学”。2000年3月，经教育部批准升格为本科院校，更名为"惠州学院"。
        </p>
    </div>
</body>
</html>
```
## 2.10 CSS浮动和清除
float：让元素浮动，取值：left(左浮动)、right(有浮动)

clear：清楚浮动，取值：left(清除左浮动)、right(清除右浮动)、both(同时清除上面的左浮动和右浮动)

### 2.10.1 CSS浮动
1. 浮动的元素，将向左或向右浮动，浮动到包围元素的边上，或上一个浮动元素的边上为止。
2. 浮动的元素，不再占空间了，并且，浮动元素的层级要高于普通元素。
3. 浮动的元素，一定是“块元素”，不管原来是什么元素。
4. 如果浮动的元素，没有指定宽度的话，浮动后它尽可能的变窄。因此，浮动元素一般要定宽和高。
5. 一行的多元素，要浮动一起浮动。

浮动的功能：可以实现将多个块元素并列排版
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 600px;
            border: 1px solid red;
            margin: 30px auto;
        }
        .box .div1{
            width: 100px;
            height: 100px;
            background-color: red;
            float: left;
        }
        .box .div2{
            width: 100px;
            height: 100px;
            background-color: green;
            float: left;
        }
        .box .div3{
            width: 100px;
            height: 100px;
            background-color: blue;
            float: left;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="div1"></div>
    <div class="div2"></div>
    <div class="div3"></div>
</div>
</body>
</html>
```
如何让包围元素，包住浮动元素?
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body,img,p{
            margin: 0px;
            padding: 0px;
        }
        .news{
            width: 800px;
            border: 5px solid #333;
            margin: 20px auto;
        }
        img{
            width: 300px;
            float: left;
            border: 1px solid #ccc;
            padding: 10px;
            background-color: #f0f0f0;
        }
        .news p{
            float: right;
            width: 460px;
            background-color: #ffff33;
        }
        .news .clear{
            clear: both;
        }
    </style>
</head>
<body>
<div class="news">
    <img width="300" src="images/05.jpg" />
    <p>
        惠州学院（Huizhou University）是广东省省属公办综合性普通本科院校，
        是广东省与惠州市共建高校，位于全国文明城市惠州。惠州学院创办于194
        6年，学校前身粤秀中学迁至惠阳丰湖书院，后改办为“广东省立惠州师范
        学校”。1978年12月，经国务...
    </p>
    <div class="clear"></div>
    <div>
        截至2017年6月，学院有全日制在校生16749人，成人教育类学生11010人；
        学校有18个二级学院，开设52个本科专业； [4]  有教师767名；学校占地
        总面积2476.1亩，校舍建筑面积38.37万平方米，绿化面积132.3万平方米，
        绿化覆盖率达到80%。学校拥有能举办世界级比赛的室内游泳馆24390平方米
        、室内体育馆12163平方米。学校拥有教学仪器设备16846.2万元，馆藏纸质
        图书163万册，电子图书99.1万册。
    </div>
</div>
</body>
</html>
``` 
### 2.10.2 CSS清除浮动
CSS清除浮动的功能有两个：
1. 可以包围元素从“视觉上”包住浮动元素
2. 清除之下的其他元素将恢复默认排版。

有浮动，就得有清除。

如果包围元素指定了高度了，那么可以不使用清除功能。

### 实战
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body,ul,li,a,img{
            margin: 0;
            padding: 0;
        }
        ul,li{
            list-style: none;
        }
        a:link,a:visited{
            color: #444;
            text-decoration: none;
        }
        a:hover{
            color: red;
        }
        body{
            font-family: 宋体;
            font-size: 12px;
            background-color: #cccccc;

        }
        /* 开学模块 */
        .kaixue{
            width: 660px;
            margin: 10px auto;
            border: 5px solid blue;
            background-color: #ffffff;
            padding: 10px 10px;
        }
        .kaixue img{
            width: 300px;
            height: 200px;
            border: none;
            padding: 10px 10px;
        }
        .kaixue li{
            border: 1px solid red;
            float: left;
            text-align: center;
        }
        .clear{
            clear: both;
        }
    </style>
</head>
<body>
<div class="kaixue">
    <u1>
        <li>
            <a href="#"><img src="images/04.jpg"/></a><br/>
            <a href="#">曹伟-玩酷我的程序人生</a>
        <li>
            <a href="#"><img src="images/05.jpg"/></a><br/>
            <a href="#">王东方-辣妈挑战APP</a>
        </li>
        <li>
            <a href="#"><img src="images/06.jpg"/></a><br/>
            <a href="#">康红红专题-因为爱情</a>
        </li>
    </u1>
    <div class="clear"></div>
</div>
</body>
</html>
```
## 2.11 CSS继承性和优先级
### 2.11.1 CSS继承性
CSS属性继承：外层元素的样式，会被内层元素进行继承。多个外层元素的样式，最终都会“叠加”到内层元素上。
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body{
            background-color: #ccc;
            font-size: 24px;
        }
        .news{
            width: 600px;
            border: 1px solid #ccc;
            margin: 20px auto;
            background: #fff;
            padding: 20px;
            color: red;
        }
    </style>
</head>
<body>
<div class="news">
    <h1>惠州学院</h1>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
    </p>
</div>
</body>
</html>
```
什么样的CSS属性能被继承呢？
1. **CSS文本属性都会被继承的**：color,font-size,font-family,font-style,font-weight,text-align,text-decoration,text-index,letter-spacing,line-height等等。

提示：<body>中的CSS属性，会被所有的子元素继承。
### 2.11.2 优先级
1. 单个选择器的优先级

行内样式>id选择器>class选择器>标签选择器
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .news .title{
            color: blue;
        }
        .news h1{
            color: red;
        }
        #title{
            color: blue;
        }
    </style>
</head>
<body>
<div class="news">
    <h1 class="title" id="title" style="color: yellow">惠州学院</h1>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
    </p>
</div>
</body>
</html>
```
2. 多个选择器的优先级

多个选择器的优先级，一般情况下指向越准确，优先级越高。<br/>
特殊情况下，我们需要假设一些值:<br/>
标签选择器   优先级为1<br/>
类选择器   优先级为10<br/>
Id选择器   优先级为100<br/>
行内样式   优先级为1000

计算以下优先级<br/>
.new h1{color:red;}优先级：10+1=11<br/>
.title{color:blue;}优先级：10

div.new h1{color:red;}优先级：1+10+1=12<br/>
h1.title{color:blue;}优先级：1+10=11
## 2.12网页布局
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 800px;
            margin: 0px auto;
            border: 1px solid #444444;
            background-color: yellow;
            padding: 10px;
        }
        .box .header{
            height: 90px;
            background-color: #6600ff;
            margin-bottom: 10px;
        }
        .box .left{
            float: left;
            width: 590px;
            height: 400px;
            background-color: #00cc00;
        }
        .box .right{
            float: right;
            width: 200px;
            height: 400px;
            background-color: #ff00ff;
        }
        .box .clear{
            clear: both;
        }
        .box .footer{
            height: 90px;
            background-color: #444444;
            margin-top: 10px;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="header"></div>
    <div class="left"></div>
    <div class="right"></div>
    <div class="clear"></div>
    <div class="footer"></div>
</div>
</body>
</html>
```
## 2.13 display属性
1. 功能：规则网页元素如何显示的问题
2. 取值：none(隐藏)、block(以块元素显示)、inline(以行内元素显示)
3. block：可以实现将行内元素转成块元素。
4. inline:可以实现将块元素转成行内元素。
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .news{
            width: 600px;
            margin: 0px auto;
            border: 1px solid #444444;
            padding: 20px;
            background-color: #f0f0f0;
            display: none;/* 隐藏 */
        }
    </style>
</head>
<body>
<div class="news">
    <h1 class="title">惠州学院</h1>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
    </p>
</div>
</body>
</html>
```
## 2.14 overflow属性：当内容溢出时，该如何显示
overflow：当内容溢出时，溢出的内容该如何显示。取值：visible(可见)、hidden(隐藏)、sroll(出现滚动条)、auto(自动)
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .news{
            width: 600px;
            height: 400px;
            margin: 0px auto;
            border: 1px solid #444444;
            padding: 20px;
            background-color: #f0f0f0;
            overflow: scroll;
        }
        .news .title{
            text-align: center;
        }
        .news p{

            font-size: 18px;
            line-height: 150%;
        }
    </style>
</head>
<body>
<div class="news">
    <h1 class="title">惠州学院</h1>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
    </p>
</div>
</body>
</html>
```
## 2.15 curse光标类型
curse:网页中光标的类型，取值：text(文本)、help(帮助)、wait(等待)、hand(不兼容，建议不用)、pointer(手形)等
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .news{
            width: 600px;
            height: 400px;
            margin: 0px auto;
            border: 1px solid #444444;
            padding: 20px;
            background-color: #f0f0f0;
            overflow: scroll;
            cursor: pointer;
        }
        .news .title{
            text-align: center;
        }
        .news p{
            font-size: 18px;
            line-height: 150%;
        }
    </style>
</head>
<body>
<div class="news">
    <h1 class="title">惠州学院</h1>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院，
        后改办为“广东省立惠州师范学校”。1978年12月，经国务院
        批准升格为专科院校，更名为“惠阳师范专科学校”。1993年
        9月，经广东省人民政府批准，在惠阳师范专科学校、惠州教育
        学院、西北纺织学院惠州分院联合办学基础上，成立专科层次
        的“惠州大学”。2000年3月，经教育部批准升格为本科院校，
        更名为"惠州学院"。
    </p>
</div>
</body>
</html>
``` 
## 2.16 CSS定位
position:元素定位方式，取值：static、fixed、relative、absolute
1. static:静态定位(默认状态、不定位)
2. fixed：固定定位。
3. relation：相对定位。
4. absolute：绝对定位。

定位方式，要与定位属性配合使用<br/>
定位坐标：指定定位的元素，偏移目标元素多远的距离
1. left：定位元素，距离目标元素左边的距离
2. top：定位元素，距离目标元素上边的距离
3. right：定位元素，距离目标元素右边的距离
4. bottom：定位元素，距离目标元素下边的距离

**1、固定定位，position：fixed；**
1. 固定定位，是相对于浏览器窗口来进行定位的定位。
2. 固定定位，不占空间，层级要高于普通元素。
3. 固定定位，如果不指定定位坐标的话，固定定位元素的位置。
4. 固定定位元素，一定是“块元素”。不管原来它是什么元素。

无论网页内容有多长，其位置一直不变
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 800px;
            border: 1px solid #444444;
            margin: 20px auto;
            padding: 20px;
        }
        .qq{
            width: 100px;
            height: 200px;
            background-color: #009900;
            position: fixed;/* 固定 */
            right: 50px;/* 距离浏览器窗口的距离 */
            top: 300px;
        }
    </style>
</head>
<body>
<div class="qq"></div>
<div class="box">
    <h1>惠州学院</h1>
    <p>惠州学院（Huizhou University）是广东省省属公办综合性普
        通本科院校，是广东省与惠州市共建高校 [1]  ，位于全国文
        明城市惠州。
    </p>
    <p>
        惠州学院创办于1946年，学校前身粤秀中学迁至惠阳丰湖书院
        ，后改办为“广东省立惠州师范学校”。1978年12月，经国务
        院批准升格为专科院校，更名为“惠阳师范专科学校”。1993
        年9月，经广东省人民政府批准，在惠阳师范专科学校
        、惠州教育学院、西北纺织学院惠州分院联合办学基础上，成立
        专科层次的“惠州大学”。2000年3月，经教育部批准升格为本科
        院校，更名为"惠州学院"。
    </p>
</div>
</body>
</html>
```
**2、相对定位，position：relative**
1. 相对定位，是相对于“==原来的自己==”进行定位。
2. 相对定位，依然占空间，层级高于普通元素。
3. 如果不指定定位坐标的话，相对定位元素的位置在原地不动。
4. 相对定位，原来是行内元素，定位后还是行内元素；原来是块元素，定位后还是块元素。
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        .box{
            width: 600px;
            border: 1px solid red;
            margin: 30px auto;

        }
        .box .div1{
            width: 100px;
            height: 100px;
            background-color: red;
        }
        .box .div2{
            width: 100px;
            height: 100px;
            background-color: green;
            position: relative;/* 相对定位 */
            left: 50px;
            top: 50px;
        }
        .box .div3{
            width: 100px;
            height: 100px;
            background-color: blue;
        }
    </style>
</head>
<body>
<div class="box">
    <div class="div1"></div>
    <div class="div2"></div>
    <div class="div3"></div>
</div>
</body>
</html>
```
提示：相对定位和绝对定位，一般情况下是配合使用

**3、绝对定位：position:absolute**
1. 相对于祖先定位元素(相对定位，绝对定位)，来进行的定位
2. 绝对定位元素，不占空间，层级要高于普通元素。
3. 如果不指定定位坐标的话，绝对定位元素的位置在原地不动。
4. 绝对定位元素是一个“块元素”

## 2.17 HTML引入CSS的方法

### 2.17.1 嵌入式

通过`<style>`标记，来引入CSS样式。<br/>
html语法格式：`<style type="text/css"></style>`<br/>
html5语法格式：`<style></style><br/>`
提示：`<style>`中的CSS样式，只能给当前网页来使用。<br/>
同一个网页中，`<style>`标记可以出现多次
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body{
            margin: 0px;
            padding: 0px;

        }
    </style>

</head>
<body>
<h1>大家好</h1>
</body>
<style>
    body{
        background-color: green;
    }
</style>
<style>
    h1{
        color: red;
        text-align: center;
    }
</style>
</html>
```
### 2.17.2 外联式
通过<link>标记，来引入一个外部的CSS文件(.CSS),这样的话，可以实现公共的CSS代码被多个网页共享。<br/>
` <link rel="stylesheet" type="text/css" href="css.public"> `<br/>
<link>标记的常用属性
1. rel:也就是引入的是什么类型的文件。取值：stylesheet
2. type:内容类型
3. href:引入的CSS文件地址<br/>
==提示：<link>标记放在<head>标记中。<br/>
同一个网页，可以使用多个外部样式文件==

.html文件
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body{
            margin: 0px;
            padding: 0px;

        }
    </style>
    <link href="my.css" type="text/css" rel="stylesheet">
</head>
<body>
<h1>大家好</h1>
</body>

<style>
    h1{
        color: red;
        text-align: center;
    }
</style>
</html>
```
.css文件
```
body{
    background-color: green;
}
```
注意：在CSS文件中，不能出现HTML标记。全部都是CSS的属性样式。
### 2.17.3 行内式(主要用于JS控制元素的样式)
每一个HTML标记，都有一些公共的属性：class、id、title、style。

HTML标记中的style属性的值，与CSS中样式一模一样。

==提示：行内样式中，CSS代码不能写得过多;==<br/>
==行内样式中，多个CSS属性不能换行，也就是一行写完。==<br/>
==行内样式优先级是最高的，比ID选择器还要高。==
## 2.18 CSS表格属性
border-collapse:表格边框线合并，取值：collapse。

在HTML中rules="all",存在兼容性问题，在IE下不识别，所以用层叠样式表
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
</head>
<body>
<table width="500" border="1" align="center" style="border-collapse: collapse">
    <tr>
        <td>&nbsp;</td>
        <td>&nbsp;</td>
        <td>&nbsp;</td>
    </tr>
    <tr>
        <td>&nbsp;</td>
        <td></td>
        <td></td>
    </tr>
    <tr>
        <td>&nbsp;</td>
        <td></td>
        <td></td>
    </tr>
</table>
</body>
</html>
```
## 2.19 盒子模型
我们可以把HTML标记，都看成是一个“盒子”。<br/>
这个“盒子”有哪些特征：**内容的宽度或高度、边框线、内填充、外边距。**<br/>
==“盒子”的总宽度：内容的宽度+边框宽度* 2+左填充 *2+左外边距 *2==<br/>

**上下外边距合并问题——这是一种现象**<br/>
什么情况下？上下外边距会合并？<br/>
上下两个块元素，如果每一个元素都指定了四个外边距，那么上下相邻的那个外边距会发生合并现象，合并后取其中较大的外边距。
```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        body{
            margin: 0px;
            padding: 0px;
            background-color: #990000;
        }
        .div1{
            width: 200px;
            height: 150px;
            background-color: red;
            margin: 50px;
        }
        .div2{
            width: 200px;
            height: 150px;
            background: blue;
            margin: 50px;
        }
    </style>
</head>
<body>
<div class="div1"></div>
<div class="div2"></div>
</body>
</html>
```
如果要实现上下两个`<div>`之间的距离为100px,该如何实现呢？
1. 上下两个`<div>`其中一个只指定margin-bottom：100px,而另一个<div>的margin-top:0px,这样子可以实现。
2. 可以在上下两个`<div>`中间，添加一个空的`<div>`，并给空`<div>`指定高度为100px,也可以实现。

## 2.20 综合案例
1. 网站的背景色、背景图
2. 网站主页的宽度：100px
3. 将所有图片素材复制到day6/images目录下。
4. 创建一个css文件，并将该css文件引入当前的HTML文件中。

==注意：一个标签可以有多个类名，用空格隔开==<br/>
如：`<div class="content float"></div> `
## 2.21 浏览器兼容性简介
一个网站在不同的浏览器下，显示的效果可能不一致，这所谓“不兼容”。<br/>
**兼容性调试，主要调试IE6、IE7、IE8、Firefox。**<br/>

IE浏览器的调试工具：IETESTer

### 2.21.1 调试—全局CSS设置
1. 清除所有标记的内外边距<br/>
如：
```
Body,ul,li,a,img,p,input{
    margin:0px;
    padding:0px;
}
```
2. 去除项目符号或编号前面的符号<br/>
如：
```
ul,ol,li{
    list-style：none;
}
```
3. 全局链接效果<br/>
如：
```
a:link,a:visited{
    color:#444;
    text-decoration:none;
}
a:hover{
    color:red;
}
```
4. 网页中所有的文字大小颜色<br/>
如：
```
body{
    font-size:12px;
    font-family:宋体;
    color:#ccc;
}
```
5. 去除图片的链接边框线<br/>
如：
```
img{
    border:0;
}
```
6. 全局类样式<br/>
如：
```
.floatL{
    float:left;
}
.floatR{
    float:right;
}
.clear{
    clear:both;
}
.blank10{
    height:10px;
    clear:both;
}
.red{
    color:red;
}
.blue{
    color:blue;
}
```
### 2.21.1 调试—常用的兼容性
**1. 实现所有浏览器主页居中**
Firefox下主页居中代码：
```
.box{
    margin:0px auto;
}
```
IE5.5下主页居中代码：
```
body{
    text-align:center;
}
```
将以上的两种代码，合在一起写：
```
body{
    text-align:center;/*IE5.5主页中居中*/
}
.box{
    margin:0px auto;
}
```
2. 单行文本上下居中
```
hl{
    height:30px;
    line-height:30px;
}
```
3. 在IE6下，左右margin会加倍，应该是IE6下的一个bug

==提示：排版时，能用padding解决的，坚决不用margin。如果实在想用的话，就使用其中一边==

**解决方案：使用display:inline;**<br/>
将块元素转成行内元素
### 2.21.3 CSS HACK
针对不同浏览器，书写不同的CSS代码的过程，称为“CSS HACK”。<br/>
也就是说：写一个CSS代码，让IE6识别，其它浏览器不识别。<br/>
下面，针对不同浏览器，有几个符号：<br/>
这些符号是在CSS属性的前面加的，用于分辨不同的浏览器版本。<br/>

“*”IE6和IE7都识别。如：
```
.box{
    *background-color:red;
}
```

“_”只有IE6识别。如：
```
box{
   _background-color:green; 
}
```

例：
```
body{
    background-color:#ccc;/* 所有浏览器都识别*/
    *background-color:red;/*IE6和IE7都识别 */
    _background-color:green;/*IE6识别*/
}
```
CSS HACK的编写顺序：Firefox——IE7——IE6

使用CSS HACK来处理IE6下，左右margin加倍问题
```
<style>
    body{
        margin:0px;
        padding:0px;
        background-color:green;
    }
    .news{
        width:200px;
        height:150px;
        background-color:yellow;
        margin:50px;/*所有浏览器都识别*/
        _margin:50px 50px 50px 25px;/*IE6识别*/
        float:left;/*左浮动*/
    }
</style>
```
注意：CSSHACK不是W3C的标准，因此，我们尽量少用。如果你调试兼容性，调试不好时，可以偶尔用一下。

