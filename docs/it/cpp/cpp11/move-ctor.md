#移动构造函数

支持移动语义，减少深拷贝操作

例子：

```
#include <iostream>

using namespace std;

class Moveable {
public:
    Moveable():i(new int(0)) {cout<<"default ctr"<<endl; ++dctrCnt;}
    Moveable(const Moveable& rhs):i(new int(*rhs.i)) {
        cout<<"cpy ctr"<<endl; 
        ++cpctrCnt;
    }
    Moveable(Moveable&& rhs):i(rhs.i) {
        rhs.i = nullptr;
        cout<<"move ctr"<<endl;
        ++movectrCnt;
    }
    ~Moveable() {cout<<"dectr"<<endl; delete i; ++dectrCnt;}
private:
    int* i;

public:
    static int dctrCnt;
    static int cpctrCnt;
    static int movectrCnt;
    static int dectrCnt;
};

int Moveable::dctrCnt = 0;
int Moveable::cpctrCnt = 0;
int Moveable::movectrCnt = 0;
int Moveable::dectrCnt = 0;

Moveable getTemp() {
    Moveable tmp;
    return tmp;
}


int main(int argc, char const *argv[])
{
    Moveable a(getTemp());
    cout<<"Default ctr cnt:"<<Moveable::dctrCnt<<endl;
    cout<<"Copy ctr cnt:"<<Moveable::cpctrCnt<<endl;
    cout<<"Move ctr cnt:"<<Moveable::movectrCnt<<endl;
    cout<<"Dectr cnt:"<<Moveable::dectrCnt<<endl;
    return 0;
}
```

拷贝/移动构造函数有3个版本：

+ Object(T&)
+ Object(const T&)
+ Object(T&&)

默认情况下，编译器会隐式生成一个移动构造函数，但是如果定义了构造函数/赋值运算符/析构函数中的一个或多个，就不会自动生成。默认移动构造函数与默认拷贝构造函数一样，都是按位拷贝。

如果定义了移动构造函数/移动赋值操作符/拷贝赋值操作符/析构函数中的一个或多个，也不会自动生成默认拷贝函数。

c++11中，拷贝构造/赋值函数和移动构造/赋值函数必须同时提供或同时不提供，才能同时提供两种语义，否则只能提供一种语义。


##异常
移动构造函数抛出异常是危险的，如果移动语义还没有完成就抛出异常会有问题。尽量编写不抛出异常的移动构造函数，加上noexcept，这样移动构造函数抛出异常时会调用`terminate()`终止程序。

`std::move_if_noexcept`如果移动构造函数没有noexcept关键字，返回左值使用拷贝语义，否则返回右值使用移动语义
