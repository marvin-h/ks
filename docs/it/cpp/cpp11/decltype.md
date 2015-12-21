#decltype

##typeid

RTTI,运行时类型识别
typeid返回type_info类型

头文件：

`<typeinfo>`

例子：

```
#include <typeinfo>
#include <iostream>
using namespace std;

struct str {
    int x = 1;
};

int main() {
    str s;
    cout << typeid(str).name() << endl;
    cout << typeid(s).hash_code() << endl;
}
```

##decltype

编译期类型推导，用于声明变量
auto是根据初始化表达式获得变量类型，decltype是以普通表达式为参数

```
int main() {
    int x{ 10 };
    decltype(x) y = 20;

    float a;
    double b;
    decltype(a + b) c;
}
```

应用：

```
#include <vector>

using namespace std;

using size_tt = decltype(sizeof(0));

int main() {
    size_tt t;
    vector<int> v;
    using vitrtype = decltype(v.begin());
}
```

##decltype推导规则

**标记表达式**，除去关键字，字面量等编译器需要使用的标记之外的程序员自定义的标记都是标记符。单个标记符对应的表达式就是标记符表达式。

`int arr[4];`，arr是标记表达式，arr[3]不是标记表达式

---
decltype(e)

+ 如果e是一个没有带括号的标记符表达式或者类成员访问表达式，decltype(e)就是e所命名的实体类型，如果e是重载函数，无法通过编译
+ 否则，假设e的类型是T，如果e是一个将亡值，decltype(e)为T&&
+ 否则，假设e的类型是T，如果e是一个左值，decltype(e)为T&
+ 否则，假设e的类型是T，decltype(e)为T

```
int i = 1;
decltype(i) a;
decltype((i)) b; //类型为int&，需要初始化 

int&& RvalRef();
int arr[5];

decltype(arr) var1; //int[5]
decltype(RvalRef()) var6 = 1; //int&&
decltype(true?i:i) var7 = i; //int&，表达式返回左值
```


##decltype与const/volatile

decltype会带走表达式的cv限制符，但是对于对象定义中的cv限制符，使用decltype进行推导时，其成员不会继承cv限制符



```
#include <type_traits>
#include <iostream>

using namespace std;

struct MyStruct
{
    int i;
};

int main() {
    const int i = 1;
    const MyStruct s;

    cout << is_const<decltype(i)>::value << endl; //1
    cout << is_const<decltype(s)>::value << endl; //1
    cout << is_const<decltype(s.i)>::value << endl; //0
}
```