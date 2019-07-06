## File类
File类的参数是文件路径

**路径**：
- 绝对路径：包括根目录的例如：G:\学习\eclipse-workspace
- 相对路径：相对于某个文件下的路径，例如：eclipse-workspace；

File类里面有两个常量，为了规范不同操作系统分隔符的不同而建立

- File.pathSeparator
- File.separator
#### File类的构造
```
public class Test1 {
	public static void main (String args[]) {
		
		String path = "G:\\学习\\eclipse-workspace\\Text\\bin\\My_Firstjava";
		String x = "Test1.class";
		//通过相对路径构造
		File f = new File(path, x);
		File f1 = new File(new File(path), x);
		System.out.println(f.getPath());
		System.out.println(f.getName());
		System.out.println(f1.getPath());
		System.out.println(f1.getName());
		//通过绝对路径构造
		File f2 = new File(path+"\\"+x);
		System.out.println(f2.getPath());
		System.out.println(f2.getName());
		//如果没有写跟盘目录：“学习\\eclipse-workspace\\Text\\bin\\My_Firstjava”；
		//则根据你当前的工作空间构建。
		File f3 = new File("Test.class");
		System.out.println(f3.getPath());//如果是绝对路径返回绝对路径。如果是相对路径返回相对路径。
		System.out.println(f3.getName());//返回文件名
		System.out.println(f3.getAbsolutePath());//返回绝对路径
	}
}
```
#### File类的常用方法
- get名字：

getName()：、getAbsolutePath()：、getPath()：

getParent():返回上一级目录，如果上一级没有返回null
- exists：判断文件是否存在，返回布尔类型
- canWrite：判断文件是都可写，不仅仅表示文件，还可以表示文件夹

canRead:判断可写
- isFile()：判断是否是文件，会自动判断是否有真实存在的文件，如果没有默认为文件夹
- isDirectory():判断是否为一个目录（判断是不是一个文件夹）
- isAbsolutePath：判断是否为绝对路径
#### 长度字节
- length():读取文件长度，只有文件可以读取
- createNewFile()：创建一个文件，返回布尔类型，创建成功返回true，反之
- delete():删除文件，返回布尔类型
- static createTempFile(前缀3个字节长, 后缀默认.temp, 目录（或者不写，会储存在默认空间）)；：生产临时文件，运行结束及删除。
- deleteOnExit():退出虚拟机删除，常用于删除临时文件
#### 操作目录
- mkdir():创建目录，必须确保父目录存在，如果不存在则创建失败
- mkdirs():创建目录，如果父目录不存在，则自动创建父目录列。
- list():输出一个目录下的文件。返回字符串
- listFiles()：将当前目录下的文件返回，用一个文件数组接收
- listRoots():获取根目录

**例子：递归实现输出目录下所有文件**
```
public static void show(File f){
		
		if(f.isFile()) {
			System.out.println(f.getName());
		}
		else if(f.isDirectory()){
			File []x = f.listFiles();
			
			for(int i = 0;i<x.length;i++) {
				show(x[i]);
			}
		}
	}
```
## IO流
什么是流：从一端移动到另一端，源头与目的地的关系。程序与文件数组|网络连接|数据库|，以程序为中心

IO流的分类：

**依据流向**：输入输出流

**依据数据（重点）**：字节流：以二进制为基础。可以处理一切文档，包括音频|
字符流：以文本文档，只能处理存文本。

**功能**：节点流---包裹源头|
处理流---增强功能，提供性能。

### 字节流和字符流
**字节流的输入输出流**：InputStream;OutputStream;

- read();+close();读入字节，关闭读入
- write();+flush();+close();读出字节，刷新缓存，关闭读出

**字符流的输入输出流**：Reader;Writer;
- read();+close();读入字符，关闭读入
- write();+flush();+close();读出字符，刷新缓存，关闭读出

#### 文件读入例子
```
public class Test1 {
	public static void main (String args[]) {
		//建立文件关系
		String path = "G:\\xxx.txt";
		File book = new File(path);
		//选择流
		InputStream it = null;
		try {
			//不断读取缓冲数组
			it = new FileInputStream(book);
			byte []num = new byte[10];
			int len = 0;
			//read可以返回读取到的字节数，如果无法读取了返回-1
			while((len = it.read(num)) != -1) {
				String temp = new String(num, 0, 10);
				System.out.println(temp);
			}
		}
		catch (FileNotFoundException e){
			e.printStackTrace();
		} 
		catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
#### 文件写出的例子
```
public class Test1 {
	public static void main (String args[]) {
		File book = new File("G://xxx.txt");
		OutputStream os = null;
		try {
			os = new FileOutputStream(book, true);//true代表继续写。false代表覆盖写。
			String temp = "过小虎好帅";
			byte []b = temp.getBytes();
			os.write(b, 0, b.length);
			os.flush();
		} 
		catch (FileNotFoundException e) {
			e.printStackTrace();
		} 
		catch (IOException e) {
			e.printStackTrace();
		}
		finally {
			if(os != null) {
				try {
					os.close();
				} catch (IOException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		}
	}
}
```
#### 字节流文件复制实例
```
public static void copyFile(String start, String dis) throws IOException {
		File s = new File(start);
		File d = new File(dis);
		
		InputStream in = new FileInputStream(s);
		OutputStream os = new FileOutputStream(d);
		
		byte []num = new byte[1024];
		int len = 0;
		while((len = in.read(num)) != -1) {
			
			os.write(num, 0, len);
			os.flush();
		}
		os.close();
		in.close();
}
```
### 处理流
缓冲字节输入流：BufferedInputStream()。没有新增方法；

缓冲字节输出流：BufferedOutputStream()。没有新增方法；

使用例子
```
InputStream in = new BufferedInputStream(new FileInputStream(s));
OutputStream os = new BufferedOutputStream(new FileOutputStream(d));
```
缓冲字符输入流：BufferedReader()。新增方法，readLine()读入一行

缓冲字符输出流：BufferedWriter()。新增方法，写出一行

**用法和字节流相似**
### 转换流
转换的过程我们会产生乱码，乱码产生的原因有编码与解码的字符集不相同和字节数不够造成的。

**编码**：字符串转成二进制；

**解码**：二进制转换成字符串

转换流有：InputStreamReader("文件, "字符集")

OutputStreamWriter("文件, "字符集")
```
BufferedReader it = new BufferedReader(
				new InputStreamReader(new FileInputStream(new File("G:\\xxx.txt")), "utf-8"));
```				
## 总结
![image](http://wx4.sinaimg.cn/mw690/0060lm7Tly1ftiffhaj2xj30e70dgac7.jpg)
![image](http://wx1.sinaimg.cn/mw690/0060lm7Tly1ftifg37mprj30nh0eyq7g.jpg)