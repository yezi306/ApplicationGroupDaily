[toc]
## 6. Object
所有类的根类

Object是不断抽取而来，具备着对所有对象的共性内容。

### 6.1 equals
```
class Person extends Object
{
    private int age;
    Person(int age)
    {
        this.age=age;
    }
}
class OjectDemo
{
    public static void main(String[]args)
    {
        Person p1=new Person(20);
        Person p2=new Person(20);
        
        System.out.println(p1==p2);          //比较地址
        System.out.println(p1.equals(p2));   //比较地址
    }
}
```

Object中equals的代码
```
public boolean equals(Object obj)
{
    return (this==obj);
}
```
### 6.3 equals覆盖(重点)
一般都会覆盖此方法，根据对象的特有内容，建立判断对象是否相同的依据。
```
class Person extends Object
{
    private int age;
    Person(int age)
    {
        this.age=age;
    }
    public boolean equals(Object obj)
    {
        if(!(obj instanceof Person))
        {
            //return false;
            throw new ClassCastException("类型错误");  //抛出一个ClassCastException类
        }
        Person p =(Person)obj;
        return (this.age==p.age);
    }
}
class OjectDemo
{
    public static void main(String[]args)
    {
        Person p1=new Person(20);
        Person p2=new Person(20);

        System.out.println(p1.equals(p2));   //比较age
    }
}
```
### 6.4 hashCope方法
`System.out.println(Integer.toHexString(p1.hashCode))。`

结果返回一个十六进制的哈希值。

### 6.5 getClass方法
```
Class clazz1=p1.getClass();
Class clazz2=p2.getClass();
System.out.println(clazz1==clazz2);   //返回true
System.out.println(clazz1.getName()); //返回Person
```
### 6.6 toString方法
任何的类都继承自Object方法，你输出对象的时候，其实是输出object的tostring方法

Object 类的 toString 方法返回一个字符串，该字符串由类名（对象是该类的一个实例）、at 标记符“@”和此对象哈希码的无符号十六进制表示组成。换句话说，该方法返回一个字符串，它的值等于： 

getClass().getName() + '@' + Integer.toHexString(hashCode())

getClass().getName()+'@'+Integer.toHexString(hashCode());
```
toString方法覆盖
class Person extends Object
{
    private int age;
    Person(int age)
    {
        this.age=age;
    }
    public boolean equals(Object obj)
    {
        if(!(obj instanceof Person))
        {
            //return false;
            throw new ClassCastException("类型错误");  //抛出一个ClassCastException类
        }
        Person p =(Person)obj;
        return (this.age==p.age);
    }
    public String toString()
    {
        return "Person:"+age;
    }
}
```