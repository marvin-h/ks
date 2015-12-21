#POD类型

POD，plain old data，通常用于说明一个类型的属性

POD类型的优点：

+ 字节赋值，可以安全的使用memset和memcpy
+ 对c内存布局的兼容，可以和c函数进行互相操作
+ 保证了静态初始化的安全有效

c++11将POD划分为两个集合：trivial和standard layout

可以通过`template<typename T> struct is_pod`来判断
头文件：`<type_traits>`

##trivial

一个trivial的类应该符合以下定义：

+   拥有trivial constructor和trivial destructor
    trivial代表什么都不干，编译生成的默认构造和析构函数就是trivial的
    自定义的构造和析构函数即使没有代码，也不是trivial的
+   拥有trivial的拷贝构造函数和移动构造函数
+   拥有trivial的拷贝赋值操作符和移动赋值操作符
+   不能有虚函数和虚基类

可用`template<typename T> struct is_trivial`判断

例子：
```
#include <type_traits>
#include <iostream>

using namespace std;

class trivial1 {

};

class trivial2 {
    int i;
};

class nontrivial1 {
    nontrivial1() {}
};

int main() {
    cout << is_trivial<trivial1>::value << endl; //1
    cout << is_trivial<trivial2>::value << endl; //1
    cout << is_trivial<nontrivial1>::value << endl; //0
    return 0;
}
```


##standard layout

标准布局的类符合以下定义：

+ 所有非静态数据成员有相同的访问权限（public/private/protected）
+ 在类继承时，满足以下两种情况之一

    + 派生类有非静态成员，且只有一个仅包含静态成员的基类
    + 基类有非静态成员，派生类没有非静态成员
    
+ 派生类中第一个非静态成员的类型与其基类不同
+ 没有虚函数和虚基类
+ 所有非静态数据成员都符合标准布局，其基类也符合标准布局

c++11中用`template<typename T> struct is_standard_layout`来判断

