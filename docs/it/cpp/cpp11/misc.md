#稳定性与兼容性

##C99兼容宏

###`__STDC_HOSTED__`

目标系统环境是否包含完整的标准C库。

+   1，包含
+   0，不包含

###`__STDC__`

编译器的实现是否和C标准一致。

###`__STDC_VERSION__`

编译器支持的C标准的版本。

###`__STDC_ISO_10646__`

C++编译器符合某个版本的ISO/IEC 10646标准。

###`__func__`

返回函数的名字。
和`__FUNCTION__`的功能一样。

###`_Pragma`

`_Pragma(string)`
与`#pragma`功能相同。

```
#pragma once
_Pragma("once")
```

###`__VA_ARGS__`

变长参数的宏定义。

```
#define PR(...) printf(__VA_ARGS__)
```


##Cpp11

###`__cplusplus`

```
#ifdef __cplusplus
extern "C" {

}
#endif
```

###静态断言

`assert`
运行期断言。

`static_assert(expr, string)`
编译期断言。

###noexcept

表示函数是否抛出异常。

两种形式：

+   noexcept(constexpr)

    如果constexpr是true，不会抛出异常。否则，可能抛出异常。

+   noexcept

    不会抛出异常。

如果函数声明不抛出异常却抛出了异常，调用std::terminate()来终止程序运行。

###快速初始化成员变量

允许使用`=`和`{}`对非静态成员变量就地初始化。

就地初始化在构造函数的初始化列表之前。

```
class Test
{
    int i = 1;
};
```


###非静态成员的sizeof

```
class Test
{
public:
    int i;
};
```

c++98:

```
sizeof(((Test*)0)->i)
```

c++11:

```
sizeof(Test::i)
```

###friend

声明友元类时可以不用class关键字，可以用别名，可以用于模板。

```
class Poly {};
typedef Poly P;

class Test
{
friend Poly;
};

class Test1
{
friend P;
};

template<typename T> class Test2
{
friend T;
};

```


###final/override

final

阻止派生类重写函数。

```
class Base
{
public:
    virtual ~Base() {}
    virtual void f() {}
};

class D : public Base
{
public:
    void f() final {}
};
```

override

函数必须重写基类的同名函数，否则编译器报错。

```
void f() override {}
```


###函数模板的默认模板参数

函数模板允许有默认模板参数。

```
template<typename T = int>
void f() {}
```

类模板的默认模板参数必须从右到左，函数模板的默认模板参数不必。
如果模板参数能被推导，则不用默认版本。


###外部模板

改进编译模板的性能。
模板实例化时会产生多次定义，需要链接器去重。

用extern声明外部模板，不会生成实例代码。

```
//test.h
template<typename T>
void f(T) {}
```

```
//test1.cpp
#include "test.h"

template void f<int>(int); //显示实例化
void test1() {f(3);}
```

```
//test2.cpp
extern template void f<int>(int); //外部模板声明，不会生成实例代码
void test2() {f(3);}
```

###局部类型和匿名类型做模板实参

局部类型和匿名类型可以做模板实参。

```
template<typename T>
void f(T) {}

typedef struct {} B;

int main()
{
    struct C {};
    B b;
    C c;
    f(b);
    f(c);
}
```