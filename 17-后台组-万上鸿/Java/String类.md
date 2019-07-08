
### 1.foreach语句
foreach语句的格式：
```
for(数据类型 变量名：数组）{
    
}
```
### 2.字符数据池
```
class InitializationTest {
    public static void main (String[] args) {
        String tony, jay;
        tony = "i am a student";
        jay = "i am a student";
        System.out.println(tony == jay);
    }
}
```
第一个程序：当执行到tony = "i am a student"时; JVM首先会去字符池中查找是否存在“i am a student”
这个对象，如果不存在，则在字符串中创建“i am a student”这个对象，然后将池中“i am a student”这个对象
的引用地址返回给字符串常量tony,这样tony会指向池中“i am a student”这个对象。如果存在，则不创建如何对象。
直接把对象“i am a student”的引用地址返回给tony。同理可知，tony的地址和jay的地址相同。所以返回结果：true；</br>
```
class Test {
        public static void main (String[] args) {
        String tony, jay;
        tony = new String("I am a student");
        jay = new String("I am a student");
        System.out.println(tony == jay);
    }
}
```
二个程序：tony = new String("I am a student");JVM首先在字符串池中查找有没有“I am a student”,如果有，则不在池中再去创建
这个对象了，直接在堆中创建一个“I am a student”字符串对象，然后将堆中的这个“I am a student”对象的地址返回赋
给引用tony,tony就指向了堆中创建的这个“I am a student”的对象。如果没有，则首先在字符池中创建一个“I am a student”字符串对象，然后在堆中创建“I am a student”字符串对象，将堆中的这个“I am a student”对象的地址返回赋
    给引用jay,这样，jony指向了堆中创建的这个“I am a student”字符串对象。当执行String jay=new String("I am a student")  时，因为采用new关键字创建对象时，每次new出来的都是一个新的对象，也即是说引用 tony和jay指向的是两个不同的对象，因此语句
    System.out.println(tony==jay)输出：false
### 3.== 和 equals的区别
判断两个字符串是否相等
1. ==

`System.out.println(a == b);`
中的a==b,a的值是数组a的首地址，b的值是数组b的首地址因为在new下，字符串不存进“数据字符池”,所以a不等于b,输出false。

2. equals

`System.out.println(a.equals(b)); `equals判断字符串是否相同，由于a和b的字符串的长度、字符相同，所以a.equals(b)为真，所以输出true
### 4.String类的equalsIgnoreCase
判断两个字符串是否相等不考虑大小写
### 5.String类中的方法
1. replace方法（转换）
```
String a1=new String("hellovorld");
String b1=a1.replace('v','w');          //将"v"转换成"w"
```
2. replaceFirst方法（第一个转换）
```
String a2=new String("he22ovorld");
String b2=a2.replaceFirst("22","21");   // 将"22"换成"21"
System.out.println(b2);     //输出结果he21oworld
```
3. split方法（分开）
```
String str=new String("从前有座山,山上有座庙,庙里有个老和尚,在讲一个故事,故事讲的是");
String []b3=str.split(",");             //将字符串（按照“,”分开）
for(String s:b3)
{
	System.out.print(s+"\t");           //用foreach语句遍历输出
	}
System.out.println("");
```
4. toLowerCase方法（转换成小写）
```
String a2=new String("he22ovorld");
String b2=a2.replaceFirst("22","21");   // 将"22"换成"21"
System.out.println(b2);     //输出结果he21oworld
```
5. toUpperCase方法（转换成大写）
```
String a5=new String("HelloWorld");
String b5=a5.toUpperCase();             //转换成大写
System.out.println(b5);                 //输出结果HELLOWORLD               //输出结果
```
6. trim方法(去除空格)
```
String a6=new String("         helloworld");
String b5=a6.trim();          //去除空格
System.out.println(b6);      //输出结果
```
### 6.StringBuffer的方法
1. append方法(追加)
```
StringBuffer buf=new StringBuffer("hello");
String str=new String("world");
buf.append(str);                                   //将"hello"和"world"追加起来
System.out.println(buf);    //输出结果helloworld
```
2. setCharAt方法(修改)
```
StringBuffer buf2=new StringBuffer("0123456789");
buf2.setCharAt(4,'x');        //将0123456789将第5个数改成X
System.out.println(buf2);    //输出结果0123x56789
```
3. insert方法(插入)
```
StringBuffer buf3=new StringBuffer("0123456789");
buf3.insert(4,'x');                                //在第五个数之前插入X
System.out.println(buf3);   //输出结果0123x456789
```
4. reverse方法(反向输出)
```
StringBuffer buf4=new StringBuffer("123456789");
buf4.reverse();            //反向输出
System.out.println(buf4);   //输出结果：987654321
```
5. delete方法(删除)
```
StringBuffer buf5=new StringBuffer("123456789");
buf5.delete(1,5);            //删除从下标为1开始，到下标为5前的字符，即删除2345
System.out.println(buf5);    //输出结果：16789
```