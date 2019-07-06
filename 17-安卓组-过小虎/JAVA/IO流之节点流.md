### 字符数组的操作
字节流的读入
```
public static void main (String args[]) throws IOException {
	String a = "过小虎好帅";
	byte []b = a.getBytes();
	InputStream is = new BufferedInputStream(new ByteArrayInputStream(b));
	byte []temp = new byte[1024];
	int len = 0;
	while(-1 != (len = is.read(temp))){
		System.out.println(new String(temp, 0, len));
	}
}
```
字节流的输出
```
public static void main (String args[]) throws IOException {
	//目的地
	byte []dis = new byte[1024];
	//选择字符流
	ByteArrayOutputStream bs = new ByteArrayOutputStream();
	//操作
	String fin = "过小虎好帅";
	byte []temp = fin.getBytes();
	bs.write(temp, 0, temp.length);
	//写出操作
	dis = bs.toByteArray();
	bs.close();
	System.out.println(new String(dis));
}
```
#### 字节流与文件流的合并应用
从文件获取字节数组
```
public static byte[] getbytearrayfromfile(String path) throws IOException {
	byte []dis = null;
	File f = new File(path);
	BufferedInputStream in = new BufferedInputStream(new FileInputStream(f));
	ByteArrayOutputStream b = new ByteArrayOutputStream();
	byte []temp = new byte[1024];
	int len = 0;
	while((len = in.read(temp)) != -1){
		b.write(temp, 0, temp.length);
	}
	dis = b.toByteArray();
	b.close();
	in.close();
	return dis;
}
```
将字节数组输出到文件中
```
public static void setfilefrombytearray(byte []src, String path) throws IOException {
	File dis = new File(path);
	ByteArrayInputStream bi = new ByteArrayInputStream(src);
	BufferedOutputStream os = new BufferedOutputStream(new FileOutputStream(dis));
	byte []num = new byte[1024];
	int len = 0;
	while((len = bi.read(num, 0, src.length)) != -1) {
		os.write(num);
	}
	os.flush();
	os.close();
	bi.close();
}
```
### 基本数据处理流
保留基本数据的输入输出，供机器识别。

讲数据读入到文档中
```
public static void out(String path) throws IOException {
	double a = 2.5;
	long b = 10L;
	String c = "gxh";
	File dest = new File(path);
	DataOutputStream d = new DataOutputStream(new BufferedOutputStream(new FileOutputStream(dest)));
	d.writeDouble(a);
	d.writeLong(b);
	d.writeUTF(c);
	d.flush();
	d.close();
}
```
讲文档中的数据读取出来
```
public static void in(String path) throws IOException {
	File dest = new File(path);
	
	DataInputStream i = new DataInputStream(new FileInputStream(dest));
	
	System.out.println(i.readDouble());
	System.out.println(i.readLong());
	System.out.println(i.readUTF());
	
}
```
**取出数据的顺序必须和存放时相同，并且文件需要保留基本数据储存，否者会出错**

**基本数据处理流也可以和字节流一起使用。讲基本数据转换成字节，将字节解码为基本数据。**
### 自定义类处理流
ObjectInputStream和ObjectOutputStream;

什么是序列化和反序列化
- 序列化就是将自定义类型转化为文件。
- - 需要实现序列化的对象需要实现Serializable接口。
- 反序列化就是将文件转换为自定义类型。
- - 不需要被序列化的成员需要加入transient关键词修饰
### 打印流
我们平时用的System.out.println就是一个打印流，PrintStream();**它属于字节流**

#### 如何向文件打印文字。
```
File f = new File("G:\\xxx.txt");
PrintStream p = new PrintStream(new BufferedOutputStream(new FileOutputStream(f)));
p.println("过小虎好帅");
p.close();
```
重定向：将System.out.print改变输出位置，例如输出到文本当中。   
```
//更改输出位置到文件中。PrintStream的第二个参数，加入true后会自动加入缓冲函数。
System.setOut(new PrintStream(new BufferedOutputStream(new FileOutputStream(f)),true));
System.out.println("爱你老王");
//如何更改回控制台输出
System.setOut(new PrintStream(new BufferedOutputStream(new FileOutputStream(FileDescriptor.out)),true));
System.out.println("back....");
```
其中**FileDescriptor.out**代表控制台输出。
#### 如何从键盘上获取值实现c++中cin的功能
```
//从键盘输入
Scanner it = new Scanner(System.in);
System.out.println(it.nextLine());
```
或者
```
InputStream it = System.in;//System.in是一个InputStream类
BufferedReader br = new BufferedReader(new InputStreamReader(it));
System.out.println(br.readLine());
```
### 装饰设计模式
IO流运用到的就是装饰设计模式

一个类对另一个类进行修饰。

类与类之间的关系
1. 依赖：形参|局部变量
2. 关联：属性
- 聚合：生命周期不一样；
- 组合：生命周期一样；
3. 继承：父子类
4. 实现：接口与实现类
# 总结
![image](http://wx1.sinaimg.cn/mw690/0060lm7Tly1ftiqtun6luj30ix0f67d9.jpg
)