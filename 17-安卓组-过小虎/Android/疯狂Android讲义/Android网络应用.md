### 基于TCP协议的网路通信
在通信的两端建立一个Socket，从而在通行的两端之间形成网络虚拟链路。**JAVA使用Socket对象来表示两端的通信接口**，并通过Socket产生IO流来进行网络通信
#### TCP协议基础
IP协议使Internet成为一个允许连接不同类型的计算机和不同操作系统的网络。**IP协议只保证计算机能发送和接受分组数据**所以为了解决传输中的其他问题，连接上Internet的计算机还需要安装TCP协议来提供可靠并且无差错的通信服务

TCP协议是一种端对端的协议，TCP协议使用重发机制：即只接收方在接收到信息以后，发出收到信号，发送方才会停止发送信息，否则发送方将不断向接收方发送信息
#### 使用ServerSocket创建TCP服务器端
ServerSocket对象用于监听来自客户端Socket连接，如果没有连接将会一直处于线程阻塞状态
- ServerSocket.accept（）：用于监听客户端是否请求，如果请求了则返回一个Socket对象，如果没有请求则一直保持堵塞状态
- ServerSocket的构造方法有3个
- - ServerSocket（int port）指定端口port来创建一个Socket
- - ServerSocket（int prot， int backlog）增加一个用来改变连接队列长度的参数
- - ServerSocket（int prot， int backlog， InetAddress localAddr）如果机器中存在多个IP地址，则可以通过第三个参数绑定一个IP地址
- ServerSocket.close（）关闭ServerSocket
#### 使用Socket进行通信
Socket的构造函数有两个
- Socket(InetAddress/String remoteAddress, int port):改方法指定了远程连接的主机IP地址和端口号，本机地址采用默认的
- Socket(InetAddress/String remoteAddress, int port, InetAddress localAddr, int localPort):增加了本机地址适用于一台电脑有多个IP地址的情况
