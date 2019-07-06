## 网络
![image](http://wx2.sinaimg.cn/mw690/0060lm7Tly1ftk42b0ut4j30fk0bs76z.jpg)
**URL和URI的区别**
URI只表示一个资源标识符，URL不仅是资源标识符还增加了定位。

**端口号用于区分计算机软件的**
### InetAddress类:没有端口
```
public static void main (String args[]) throws UnknownHostException {
	InetAddress it = InetAddress.getLocalHost();//获取本机
	System.out.println(it.getHostName());//输出本机名字
	System.out.println(it.getHostAddress());//输出本机IP
	it = InetAddress.getByName("www.baidu.com");//获取网址
	System.out.println(it.getHostName());
	System.out.println(it.getHostAddress());
	it = InetAddress.getByName("1.2.3.4");//如果IP有效转换为网址输出，如果无效则按原来的输出
	System.out.println(it.getHostName());
	System.out.println(it.getHostAddress());
}
```
### InetSocketAddress类：含有端口。
```
public static void main (String args[]) throws UnknownHostException {
	InetSocketAddress is = new InetSocketAddress("www.baidu.com",100);//有构造函数
	System.out.println(is.getPort());
	System.out.println(is.getAddress());
	InetAddress ia = is.getAddress();
	System.out.println(ia.getHostAddress());
	System.out.println(ia.getHostName());
}
```
### URL
资源表示符（URL）由4部分组成：协议、域名、端口、资源文件名
### 简单爬虫
```
public class Test1 {
	public static void main (String args[]) throws UnsupportedEncodingException, IOException {
		URL url = new URL("http://www.baidu.com");
		BufferedReader br = new BufferedReader(new InputStreamReader(url.openStream(),"utf-8"));
		BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream("G:\\frist.html"),"utf-8"));
		String temp = null;
		while((temp = br.readLine())!=null) {
			bw.append(temp);
			bw.newLine();
		}
		bw.flush();
		bw.close();
		br.close();
	}
}
```
### UDP通信原理
UDP通信是面向数据的，它不安全，就是数据去找服务器端口。很容易丢失
```
服务器端：

public static void main (String args[]) throws IOException {
		//1.创建服务器
		DatagramSocket f = new DatagramSocket(7777);//参数为服务器的端口
		//2.准备接受数据
		byte []contain = new byte[1024];
		//3.打包数据
		DatagramPacket packet = new DatagramPacket(contain, contain.length);
		//4.接受数据
		f.receive(packet);
		//5.分析数据
		byte []temp = packet.getData();
		int len = packet.getLength();
		System.out.println(new String(temp, 0, len));
		//6.释放
		f.close();
	}
```
```
客户端

public class Kehuduan {
	
	public static void main (String args[]) throws IOException {
		//1.创建客户端+端口
		DatagramSocket k = new DatagramSocket(6666);
		//2.准备数据
		String msg = "gxh";
		byte []msgb = msg.getBytes();
		//3.打包数据
		DatagramPacket b = new DatagramPacket(msgb, msgb.length, new InetSocketAddress(InetAddress.getLocalHost(),7777));
		//4.发送
		k.send(b);
		k.close();
	}
}
```
### TCP通信原理
面向连接的通信，安全性高，需要请求和相应连接。
#### Socket编程
Socket编程就是基于TCP通信原理
```
服务器：

public static void main (String args[]) throws IOException {
	//1.创建服务器
	ServerSocket f = new ServerSocket(8888);
	//2.接收客户端连接、阻塞式
	Socket s = f.accept();
	System.out.println("一个客户端建立");
	//3.发送数据
	String m = "欢迎登陆";
	DataOutputStream w = new DataOutputStream(s.getOutputStream());
	w.writeUTF(m);
	w.flush();
}
```
```
客户端：

public static void main (String args[]) throws IOException {
	//1.建立客户端
	Socket s = new Socket(InetAddress.getLocalHost(),8888);
	//2.接收数据
	DataInputStream i = new DataInputStream(s.getInputStream());
	System.out.println(i.readUTF());
}
```
### Http响应格式
1）协议版本、状态代码、描述

2）响应头

3）响应正文
```
HTTP/1.1 200 OK
//    协议版本、状态代码、描述
//    "200" : OK
//    "302" : Found 重定向.
//    "400" : Bad Request 错误请求，发出错误的不符合Http协议的请求
//    "403" : Forbidden 禁止
//    "404" : Not Found 未找到。演示访问一个不存在的页面看报文
//    "500" : Internal Server Error 服务器内部错误。演示页面抛出异常。
//    "503" : Service Unavailable。一般是访问人数过多。
Server:Apache Tomcat/6.0.12
//    服务器类型
Date:.....//日期
Content-type:text/html;charset=GBK;
//传输数据类型，编码方式
Content-length:XXX
//正文长度字节长度

//注意这里换行
响应正文
```


