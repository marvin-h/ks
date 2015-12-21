#std::forward

完美转发，指在函数模板中，完全依照模板的参数类型，将参数类型传递给函数模板调用的另一个函数。
用于模板编程，恢复模板参数的引用性

```
template<typename T>
void iamforward(T t) {func(t);}
```

`iamforward`，转发函数
`func`，目标函数

为了防止拷贝操作，通常会用引用
```
void func(int& t);
template<typename T>
void iamforward(const T& t) {func(t);} //常量左值引用不能赋给非常量左值引用
```

##引用折叠

```
typedef const int T;
typedef T& TR;
TR& v = 1;
```

<table>
<tr><td>TR的类型定义</td><td>声明类型</td><td>实际类型</td></tr>
<tr><td>T&</td><td>TR</td><td>A&</td></tr>
<tr><td>T&</td><td>TR&</td><td>A&</td></tr>
<tr><td>T&</td><td>TR&&</td><td>A&</td></tr>
<tr><td>T&&</td><td>TR</td><td>A&&</td></tr>
<tr><td>T&&</td><td>TR&</td><td>A&</td></tr>
<tr><td>T&&</td><td>TR&&</td><td>A&&</td></tr>
</table>

规则：

+ T& + & => T&
+ T&& + & => T&
+ T& + && => T&
+ T&& + && => T&&


模板函数要保留左右值引用性，需将参数声明为T&&
如果声明为T, 会失去引用性
如果声明为T&,不能匹配右值引用

+ T会保持const/volatie修饰
+ `T&& t` 形参中的t始终是左值引用，即使实参是右值引用

例子：
```
#include <iostream>
#include <utility>
using namespace std;

class A {};

A& lRef() {static A a; return a;} // lvalue ref
const A& clRef() {static A a; return a;} // const lvalue ref
A rRef() {return A();} // rvalue ref
const A crRef() {return A();} // const rvalue ref

template<typename T> 
struct TypeName {
    static const char* get() {return "Type";}
};

template<typename T>
struct TypeName<const T> {
    static const char* get() {return "const Type";}
};

template<typename T>
struct TypeName<T&> {
    static const char* get() {return "Type&";}
};

template<typename T>
struct TypeName<const T&> {
    static const char* get() {return "const Type&";}
};

template<typename T>
struct TypeName<T&&> {
    static const char* get() {return "Type&&";}
};

template<typename T>
struct TypeName<const T&&> {
    static const char* get() {return "const Type&&";}
};

template<typename T>
void printVal(T&& t) {
    cout<<TypeName<T>::get()<<endl;
}

template<typename T>
void f() {
    printVal(t);
}
```

```
int main(int argc, char const *argv[])
{
    f(lRef());
    f(clRef());
    f(rRef()); 
    f(crRef());
    return 0;
}
```

输出：

```
Type&
const Type&
Type&
const Type&
```

改为：

```
template<typename T>
void f(T&& t) {
        printVal(forward<T>(t));
}

```

输出：
```
Type&
const Type&
Type
const Type
```