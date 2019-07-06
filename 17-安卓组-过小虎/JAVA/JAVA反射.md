<font size = "4">

[toc]

### 什么是反射
Java反射就是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意方法和属性；并且能改变它的属性。而这也是Java被视为动态语言的一个关键性质

### 反射能做什么
我们知道反射机制允许程序在运行时取得任何一个已知名称的class的内部信息，包括包括其modifiers(修饰符)，fields(属性)，methods(方法)等，并可于运行时改变fields内容或调用methods。那么我们便可以更灵活的编写代码，代码可以在运行时装配，无需在组件之间进行源代码链接，降低代码的耦合度；还有动态代理的实现等等；但是需要注意的是反射使用不当会造成很高的资源消耗！

### 得到 Class 的三种方式
```
//1、通过对象调用 getClass() 方法来获取,通常应用在：比如你传过来一个 Object
//  类型的对象，而我不知道你具体是什么类，用这种方法
　　Person p1 = new Person();
　　Class c1 = p1.getClass();
        
//2、直接通过 类名.class 的方式得到,该方法最为安全可靠，程序性能更高
//  这说明任何一个类都有一个隐含的静态成员变量 class
　　Class c2 = Person.class;
        
 //3、通过 Class 对象的 forName() 静态方法来获取，用的最多，
 //   但可能抛出 ClassNotFoundException 异常
 　　Class c3 = Class.forName("com.ys.reflex.Person");
```
### 通过 Class 类获取成员变量、成员方法、接口、超类、构造方法等
1. getName()：获得类的完整名字。
2. getFields()：获得类的public类型的属性。
3. getDeclaredFields()：获得类的所有属性。包括private 声明的和继承类
4. getMethods()：获得类的public类型的方法。
5. getDeclaredMethods()：获得类的所有方法。包括private 声明的和继承类
6. getMethod(String name, Class[] parameterTypes)：获得类的特定方法，name参数指定方法的名字，parameterTypes 参数指定方法的参数类型。
7. getConstructors()：获得类的public类型的构造方法。
8. getConstructor(Class[] parameterTypes)：获得类的特定构造方法，parameterTypes 参数指定构造方法的参数类型。
9. newInstance()：通过类的不带参数的构造方法创建这个类的一个对象。
</font>