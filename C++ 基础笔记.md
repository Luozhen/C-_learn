## C++ import 与 include 的区别

import 导入库，不属于标准C++语法

include表示导入库或者头文件，为C++标准语法

------

## C++ string length() 与 size()区别

C++标准库中的string中两者的源代码如下：
~~~C++
  size_type   __CLR_OR_THIS_CALL   length()   const   
  { //   return   length   of   sequence   
      return   (_Mysize);   
  }   
  size_type   __CLR_OR_THIS_CALL   size()   const   
  { //   return   length   of   sequence   
      return   (_Mysize);   
  } 
~~~
所以两者没有区别。

length是因为沿用C语言的习惯而保留下来的，string类最初只有length，引入STL之后，为了兼容又加入了size，它是作为STL容器的属性存在的，便于符合STL的接口规则，以便用于STL的算法。

string类的size()/length()方法返回的是字节数，不管是否有汉字。

------

## C++ 对象查看类型

使用typeid函数，该函数在typrinfo头文件里

~~~C++
#include <typeinfo>
using namespace std;
int main(){
	int a;
	cout << typeid(a).name() << endl;
}
~~~

------

## C++ 查找某个字符串中是否存在某字符

方法1:使用strchr(string， char)函数，该函数包含在string.h库中

方法2:使用C++ string头文件中字符串类自带的find()函数

方法2中有一个重要点需要注意，本宝宝被坑了两次。。。。

其方法原型为

~~~C++
size_t find (const string& str, size_t pos = 0) const;
~~~

注意，这里的返回值是size_t类型的，其描述的是size，为无符号整型。如果找到则返回第一个找到的位置，如果未找到，则返回-1，但注意返回的是size_type类型的，并且在字符串配置器中描述的为无符号整型，于是这个-1会转化为整型无符号最大值。
~~~C++
string a = "aX";
if(a.find('+'))
    cout << "find +" << endl;
else
    cout << "not find" << endl;
~~~
像上面这样直接调用a.find，最后还是会输出“find +”因为返回的-1是个很大的数。所以要改变这种bug，最好的使用方法是a.find("") != string::npos。
~~~C++
string a = "aX";
if(a.find('+') != string::npos)
    cout << "find +" << endl;
else
    cout << "not find" << endl;
~~~
------

## C++ 随机数生成

使用rand()函数，需添加头文件#include<cstdlib>
~~~C++
#include <iostream>
#include <cstdlib>
using namespace std;
int main(){
	srand(time()); // 设置随机种子
	cout << rand() * 5 << endl; // 生成0-4之间的数
	return 0；
}
~~~
------

## C++ 字符串操作

比较两个字符串，不区分大小写：stricmp。包含在头文件string.h 或 cstring 中

当s1<s2时，返回值 -1

当s1=s2时，返回值=0

当s1>s2时，返回值 1

这个函数之前知道，但是一直没怎么用，直到一道简单的字符串操作题出来，姐姐我单纯地用人工方式循环比较出来，看到有大牛只用该函数后一行代码出结果的我，无语凝噎。。。。

------

## C++ 常用数学函数

swap() 函数：交换所传两个参数的值，函数执行后参数原来的值交换。