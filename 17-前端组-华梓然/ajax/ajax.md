# AJAX
### XMLHttpReque

浏览器内建对象，用于在后台与服务器通信（交换数据），由此实现对网页的部分更新，而不是刷新整个页面。
# 请求
### 请求行
由请求方式、请求URL和协议版本构成
### 请求头
Host：localhost 请求的主机
Cache-Control：max-age=0 控制缓存
Accept：接受的文档MIME类型
Referer：从哪个URl跳转过来的
Accept-Encoding：可接受的压缩格式
### 请求主体
即传递给服务端的数据
当以post形式提交表单的时候，请求头里会设置
Content-Type:application/x-www-form-urlencoded 以get形式当不需要

### 响应/响应报文

响应服务器发出响应，其规范格式为：状态行、响应头、响应主体

# API详解

xhr.open() 发起请求，可以是get、post方式

Xhr.setRequestHeader() 设置请求头
Xhr.send() 发送请求主体get方式使用xhr.send(null)

Xhr.onreadystatechange = function (){}
监听响应状态

Xhr.readyState = 0 时  UNSENT open 尚未使用

Xhr.readyState = 1 时  OPENED open 已调用

Xhr.readyState = 2 时  HEADERS_RECEIVED 接收到头信息

Xhr.readyState = 3 时  LOADING 接受到响应主体

Xhr.readyState = 4 时  DONE 响应完成

Xhr.status 表示响应码，如200

Xhr.statusText 表示响应信息，如OK

Xhr.getAllResponseHeaders() 获取全部响应头信息

Xhr.getResponseHeader(‘key) 获取指定头信息 如Server

Xhr.responseText\  xhr.responseXML 都表示响应主体

# 代码示例
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
        <style>
            h3{
                font-size: 28px;
                text-align: center;
            }
        </style>
    </head>
    <body>
    <h3>XMLHTTpRequest</h3>
    <p id="display"></p>
    <script>
        var xhr = new XMLHttpRequest();
        //设置了请求行 方式+地址+是否异步，true
        xhr.open('post','index.html');
        //设置请求头
        xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
        //设置请求主体
        xhr.send('username=itcast&pass=123');
    
        //接受服务器响应
        xhr.onreadystatechange = function () {
            if(xhr.readyState == 4 && xhr.status == 200
    ){
                console.log(xhr.responseText);
                document.querySelector('#display').innerHTML = xhr.responseText;
            }
        }
    </script>
    </body>
    </html>

# Get方式传参

Xhr.open(‘get’,’index.html?name=zr&age=20’)
在请求的地址后加？然后接上参数
Xhr.send(null);

