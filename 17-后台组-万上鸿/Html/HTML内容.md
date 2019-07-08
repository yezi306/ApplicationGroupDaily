<toc>

# 1.语义标签
## 1.1 常用语义标签
<nav>导航

<header> 页眉

<footer>页脚

<section>区块

<article>文章

<aside>侧边栏

progress进度条（存在很大的兼容性问题）

```
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <style>
        header {
            height: 100px;
            width: 980px;
            margin: 0 auto;
            border: 1px solid;
        }
        nav {
            background-color: red;
        }

        section {
            height: 600px;
            width: 980px;
            margin: 0 auto;
            background-color: pink;
        }

        article {
            width: 800px;
            height: 100%;
            float: left;
            background-color: blue;
        }
        aside {
            width: 180px;
            float: right;
            height: 100%;
        }
        footer {
            text-align: center;
        }

        progress {
            height: 100px;
            background-color: blue;
            /* border: 0 none;*/
            border-radius: 5px solid red;
        }
    </style>
</head>
<body>
    <!-- 使用方法跟普通标签一样，只是体现语义 -->
    <header>
        <nav>
            <a href="#">首页</a>
            <a href="#">新闻</a>
            <a href="#">资讯</a>
        </nav>
    </header>
    <section class="container">
        <article>
            主体文章
            <progress min="0" max="100" value="80"></progress>
        </article>
        <aside>
            <a href="#">其他文章</a>
        </aside>
    </section>
    <footer>
        <p>版权所有传智播客</p>
    </footer>
</body>
</html>
```
