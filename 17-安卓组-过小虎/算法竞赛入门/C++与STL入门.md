<font size = "4">

[toc]

### 引用
引用即为一个数据的别名，即为同一个东西。

使用“&”符号声明引用变量
```
#include<iostream>
using namespace std;
void swap1(int &a, int &b)
{
	int temp;
	temp = a;
	a = b;
	b = temp;
}
int main ()
{
	int a = 3, b = 5;
	cout<<"a="<<a<<"\t"<<"b="<<b<<endl;
	swap(a, b);
	cout<<"a="<<a<<"\t"<<"b="<<b<<endl;
	return 0;
} 
```
系统为我们提供了swap函数。并且功能更加强大。
### 字符串
```
#include<iostream>
#include<string>
#include<sstream>
using namespace std;
int main ()
{
	string line;
	while(getline(cin,line))
	{
		int sum = 0, x;
		stringstream ss(line);
		while(ss >> x)	sum += x;
		cout<<sum<<endl;
	}
	return 0;
}
```

---

- ==getline()读取一行字符串，可以读入空格==，普通的cin>>string是不能读入空格的，使用方法
> getline(cin, string);
- swap()用于交换两个字符串，使用方法
> a.swap(b);
- insert();指定位置插入指定字符串
> insert(num, string):在num位置前插入一个string

> insert(num1, string, num2, count):在num1位置前插入string从num2起的count个字符
- ==find():查找==从头开始查找，如果找到字串则返回字串的第一个字符的位置，==如果没找到这返回无符号整数(初始为-1)==。
- ==rfind():逆向查找==和find一样，不过是从尾部找起。
> a.find(b);查找字串b的位置
> a.find(b, num);从a的第num个位置开始查找b。

---
### 排序Sort
```
#include<iostream>
#include<algorithm>
using namespace std;
bool cmp(int x, int y){
    return x>y;
}
//传入sort使其变为升序
int main ()
{
	int num[5] = {2,1,4,3,0}, i;
	sort(num,num+5);
	for(i = 0;i<5;i++)
	{
		cout<<num[i]<<" ";
	}
	int index = lower_bound(num, num+5, 1)-num;
	cout<<"\n"<<index;
	return 0;
}
```
---

==升序：sort(begin,end,less<泛型>());==

==降序：sort(begin,end,greater<泛型>()).==
- is_sorted():判断是否排好序；
- 两个函数都属于头文件<algorithm>中
- sort可以用来排序
- lower_bound用来查找第一个大于或者等于x的地址
---

**字符排序**
```
string s = "123456";
sort(s.begin(), s.end());
cout<<s<<endl;
//正向排序 升序 
sort(s.begin(), s.end(), greater<char>());
cout<<s<<endl;
// 降序 
sort(s.rbegin(), s.rend());
cout<<s<<endl;
//反向迭代器法，降序 
```
**结构体排序**
```
struct link
{
    int a,b;
};
bool cmp(link x,link y)
{
    if(x.a==y.a)
        return x.b>y.b;
    return x.a>y.a;
}
int main()
{
    link x[4];
    for(int i=0;i<4;i++)
        cin>>x[i].a>>x[i].b;
    sort(x,x+4,cmp);
}
```
### 不定长数组——vector
常用==初始化==
```
1. 

int a[5] = {1,2,3,4,,5};
vector<int> num(a, a+sizeof(a)/sizeof(int));//使用数组初始化

2.

vector<int> num(10, 1);     //初始化为10个1，如果没有第二个参数，则为开辟10的大小。
```
---

- clear()清空数组
- resize()改变大小
- push_back()尾部添加元素
- pop_back()尾部删除元素
- empty()测试是否为空

---
```
int main ()
{
	vector<int> v;
	v.push_back(1);
	v.push_back(2);
	v.push_back(3);
	int i;
	for(i = 0;i<v.size();i++){
		cout<<v[i]<<' ';
	}
	sort(v.begin(), v.end());
	for(i = 0;i<v.size();i++){
		cout<<v[i]<<' ';
	}
}
```
### set集合
set集合容器：里面只能放入不重复的数据，并且自动排序（默认从小到大排序）
```
#include<set>
int main ()
{
	set<int> s;
	s.insert(1);
	s.insert(5);
	s.insert(2);
	s.insert(1);
	set<int>::iterator it = s.begin();
	for(;it!=s.end();it++)
	{
		cout<<*it<<' ';
	}
	//删除操作
	s.erase(s.begin());
	for(set<int>::iterator it = s.begin();it!=s.end();it++)
	{
		cout<<*it<<' ';
	}
	//erase可以删除一段地址的值。也可以指定删除某一个数
	
	return 0;
}
```
- 并集：set.union(s),也可以用a|b计算
- 交集：set.intersection(s)，也可以用a&b计算
- 差集：set.difference(s)，也可以用a-b计算
begin():返回set容器的第一个元素

end():返回set容器的最后一个元素

clear():删除set容器中的所有的元素

empty():判断set容器是否为空

max_size():返回set容器可能包含的元素最大个数

size():返回当前set容器中的元素个数

count():用来查找set中某个某个键值出现的次数

find()：返回给定值值得定位器，如果没找到则返回end()
### map映射
从键到值的映射
```
#include<map>
int main ()
{
	map<string, int> name;
	//插入操作
	name.insert(pair<string,int>("gxh",1));
	string temp;
	int i = 3;
	while(i--)
	{
		cin>>temp;
		if(!name.count(temp))	name[temp] = 0;
		name[temp]++;
		cout<<name[temp]<<endl;
	}
	//删除操作
	name.erase(name.begin());
	//erase可以删除一段地址的值。也可以指定删除某一个键值
	return 0;
}
```
### 堆栈、队列、优先队列
#### Stack栈
栈的三个操作
```
	stack<int> s;
	s.push(1);
	s.push(2);
	cout<<s.top()<<endl;
	s.pop();
	cout<<s.empty()<<endl;
```
#### queue队列
```
    queue<int> s;
	s.push(1);
	s.push(2);
	s.push(3);
	cout<<s.front()<<' '<<s.back()<<endl;
	s.pop();
	cout<<s.front()<<' '<<s.back()<<s.size()<<endl;
	s.pop();
	cout<<s.empty()<<endl; 
	s.pop();
	cout<<s.empty()<<endl; 
```
#### 优先队列priority_queue

==头文件在<queue>中==， 初始化可以用一个适当类型初始化
```
    int a[5] = {5,2,1,3,8};
	priority_queue<int> s(a, a+sizeof(a)/sizeof(int));
	s.push(1);
	cout<<s.top()<<' '<<s.size()<<endl;
	s.pop();
	cout<<s.top()<<endl;
```
优先队列可以定义比较函数，==默认是最大值在队首==。
```
    int a[5] = {5,2,1,3,8};
	vector<int> x(a, a+sizeof(a)/sizeof(int));
	priority_queue<int, vector<int>, greater<int> > s(x.begin(), x.end());
	//如果需要将其变为最小值在首，需要将泛型的3个参数全部写出。并传入greater<>。
	cout<<s.top()<<' '<<s.size()<<endl;
	s.pop();
	cout<<s.top()<<endl;
```
### 堆
堆的操作是调制一个数组或者string或者vecotr为一个堆的顺序：
```
    int a[10] = {2,10,3,6,8,12,1,6,7,5};
	vector<int> s(a, a+sizeof(a)/sizeof(int));
	for(int i = 0; i<s.size(); ++i)	cout<<s[i]<<' ';
	cout<<endl;
	make_heap(s.begin(), s.end());						//最大堆 
	//make_heap(s.begin(), s.end(), greater<int>());	//最小堆 
	for(int i = 0; i<s.size(); ++i)	cout<<s[i]<<' ';
```
==注意：只是调整了vector等的元素位置使其成为堆，用户自己有可能会改动使其又不能成为堆==，这个时候需要在调用一次make_heap使其成为堆

**堆的操作：**

**插入：**

1. 使用push_back向原来的容器的末尾添加需要插入的元素
2. 使用push_heap(s.begin(), s.end());维护堆，使其再一次成为一个堆

**删除：**

1. 首先调用pop_heap(s.begin(), s.end())将==堆顶的元素放在容器的末尾，并确保原来的顺序还在一个堆==。
2. 在调用pop_back();删除容器末尾的元素

**判断是否为堆：**
```
if(is_heap(numbers.begin(),numbers.end()));
```

**堆排序**

使用sort_heap(s.begin(), s.end())可以将一个推进行排序。

### next_permutation下一个排列
头文件<algorithm>

与之相反的函数是==prev_permutation求上一个排列==， 可以遍历全排列
```
while(next_permutation(num, num+len)){
    cout<<num<<endl;
}
```
全排列函数会判断是否还有下一个排列，并且原地改变为下一个排列。当next_permutation 没有下一个排列的时候会返回false并且自动变为升序，（也就是进入下一次的循环）
#### 不同类型的全排列使用
**int型**
```
int num[10];
while(next_permutation(num, num+10)){
    
}
```
**string型**
```
string ch = "123";
sort(ch.begin(), ch.end());//必要的时候需要进行排序
while(next_permutationg(ch.begin(), ch.end()){
    
}
```
**vector型**
```
vector<int> num(10);
while(next_permutationg(num.begin(), num.end()){
    
}
```
prev_permutation也是一样的使用方法。
</font>