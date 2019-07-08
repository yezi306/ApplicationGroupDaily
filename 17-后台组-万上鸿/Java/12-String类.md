[toc]
## 1.String类
### 1.1String
字符串是一个特殊的对象。</br>
字符串对象一旦被初始化就不会改变了。

String s="abc";：创建一个字符串对象在常量字符池中

String s1=new String("abc");；创建两个对象一个new一个字符串对象在堆内存中。

字符池中如果没有，就在池中建立，池中有，直接用
### 1.2. String 构造函数
byte []arr ={65,66,67,68};</br>
String s1=new String(arr);

以上是将字节码转化成字符串

char []c={'a','b','c''d'};
String s=new String(c,1,3);

以上是将字符数组转化成字符串：从下标为1，开始3个
### 1.3. String类——获取功能
#### 1.3.1 获取字符串长度的思想对字符串功能分类。</br>
int length();
#### 1.3.2 根据位置获取字符。</br>
char charAt(int index);
#### 1.3.3 根据字符获取在字符串中的第一次出现失误位置。</br>
int indexOf(int ch);</br>
int indexOf(int ch,int fromIndex);从指定位置进行ch的查找第一次出现位置</br>
int indexOf(String str);</br>
int indexOf(String str,int fromIndex);</br>

lastIndexOf(int ch)  </br>
int lastIndexOf(int ch, int fromIndex) </br>
int lastIndexOf(String str) </br>
int lastIndexOf(String str, int fromIndex)</br> 
#### 1.3.4 获取字符串中的一部分字符串。也叫子串
String substring(int beginIndex,int endIndex);</br>
String substring(int beginIndex);
### 1.4.转换
#### 1.4.1 将字符串变成字符串数组(字符串的切割)
String [] arr=s.sqlit(",");</br>
#### 4.2 将字符串变成字符数组
char [] chs=s.toCharArray();</br>
#### 4.3 将字符串变成字节数组
byte[] b=s.getBytes();
#### 4.4 将字符串中的字母转成大小写
String stu =str.toUpperCase();大写</br>
String stu =str.toUppetoLowerCase();大写
#### 4.5 将字符串中的内容进行替换
String stu=str.replace('a','b');
#### 4.6 将字符串两端的空格去除。
String stu=str.trim();
#### 4.7 将字符串进行连接
String stu=str.concat(str2);
### 5. 比较
str1.compareTo(str2);
### 6.判断
#### 6.1 两个字符串内容是否相同？
boolean flag=str.equals(Objcet obj);</br>
boolean flag=str.equalsIgnoreCase(Objcet obj);
#### 6.2 字符串中是否包含指定的字符串?
boolean flag=str.contains(str2);
#### 6.2 字符串是否指定字符串开头，是否以指定的字符串结尾。
boolean flag=startsWith(str);
boolean flag=endsWith(str);
### 7. intern
String s1=new String("abc");

String s2=s1.intern();
## 2.StringBuilder
和StringBuffer的区别：
1. StringBuffer是线程同步的
2. StringBuilder是线程不同步的

JDK的升级：
1. 简化书写
2. 提高效率
3. 增加安全性

StringBuffer：就是字符串缓冲区。</br>
用于存储数据的容器。</br>
特点：
1. 长度的可变的
2. 可以存储不同类型数据
3. 最终要转成字符串进行使用
4. 可以对字符串进行修改


既然是一个容器对象。应该具备什么功能呢？
1. 添加：</br>
StringBuffer stbf=stbf1.append(data);</br>
StringBuffer stbf=stbf1.insert(index,data);
2. 删除：</br>
StringBuffer delete(start,end);包含头，不包含尾</br>
StringBuffer deleteCharAt(int index);删除指定位置的元素
3. 查找
char c=stbf1.charAt(index);</br>
int c=stbf1.indexOf(String);</br>
int c=stbf1.lastIndexOf(string);
4. 修改
5. StringBuffer stbf=stbf1.replace(Start,end,string);</br>
void setCharAt(index,char);



