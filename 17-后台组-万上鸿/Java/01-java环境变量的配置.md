## 1.1 dos命令行
1. dir:(directory 目录)列出当前目录的文件以及文件夹；
2. md:(make directory创建目录)；
3. rd:(remove directory 删除目录)；注意：目录下必须为空，不可以用于删除txt等等文件。
4. cd:(change directory 改变目录)；
5. cd.. :退回根目录；
6. del:(delete删除)删除文件（如：txt等等文件，*txt ；
7. exit：退出dos命令行。

## 1.2 java语言的三种技术架构
1. J2EE  企业版:用于开发企业环境下的应用程序
2. J2SE  标准版：开发普通桌面和商务应用程序
3. J2ME  小型版：开发电子消费产品和嵌入式设备
java5.0版本后，更名为JAVAEE      JAVASE   JAVAME

## 1.3 java语言的特点：跨平台性
可以在不同的系统平台上运行<br/>
步骤：先安装一个java虚拟机（JVM）</br>
Window系统用win版的JVM</br>
Linux系统用lin版的JVM</br>
MAC系统用mac版的JVM</br>

## 1.4 java环境搭建
### 1.4.1什么是JRE，JDK
JRE ：java运行环境，包含java虚拟机和java程序核心类库</br>
JDK :java开发工具包，提供给java开发人员使用，包含java开发工具，和JRE。</br>
++编译工具（javac.exe) 打包工具（jar.exe)++
### 1.4.2下载JDK
[Oracle官网](https://www.oracle.com/)</br>
[java.sum.com](https://java.sum.com/)

### 1.4.3 环境变量配置
JAVA_HOME :....\jdk-(jdk的目录)</br>
Path:%JAVA_HOME%\bin;C:\WINDOWS.....</br>

打开DOS命令行,任意目录下敲入javac，如果出现javac的参数信息，配置成功。

### 1.4.4 classpath路径配置
set classpath=文件路径</br>
javac 文件名.java;      (java虚拟机先找该文件下的java文件)
DOS命令行下要注意结尾不要加分号;

### 1.4.1 程序中的类问题
1. 一个程序中可以有多个类
2. 每个类中最多只有一个main主函数
3. 源文件中有一个public修饰的类时，源文件的名称必须和public修饰的类的类名完全一致(区分大小写)。
4. 当一个java文件中有一个public修饰的类和一个普通类，编译后会有两个相当于的 :类.class文件。