#lambda

匿名函数，代表lambda演算

##语法

`[capture] (parameters) mutable -> returntype {statements}`

+ `[capture]` 捕捉列表，能够捕捉上下文的变量供lambda函数使用
+ `(parameters)` 参数列表，如果不需要参数，可以连同括号一起省略
+ `mutable` 修饰符，默认情况下，lambda函数是一个const函数，mutable取消常量性。使用该修饰符是，参数列表不能省略
+ `-> returntype` 返回类型，不需要返回值时，可以省略，在返回值明确的情况下也可省略，让编译器推导
+ `{statements}` 函数体

```
#include <iostream>

using namespace std;

int main() {
    auto f = [] {cout << "lambda" << endl; };
    f();
    auto f1 = [](int a, int b) {return a + b; };
    int c = f1(2, 3);
}
```

###[capture]

+ [var] 按值传递捕捉变量var
+ [=] 按值传递捕捉所有父作用域变量，包括this
+ [&var] 按引用传递捕捉变量var
+ [&] 按引用传递捕捉所有父作用域变量，包括this
+ [this] 按值传递捕捉当前this

可以组合使用

`[=,&a,&b]` a和b按引用捕捉，其他按值捕捉

不允许重复捕捉

`[=, a]` 重复捕捉了a


###特性

传值和传引用的行为有些不同
按值传递时，捕捉列表的值在定义时就确定了，按值传递时，值是常量，声明为mutable才可以修改

```
int main() {
    int x = 10;
    auto byval = [=] {return x + 1; };
    auto byref = [&] {return x + 1; };

    int ret = 0;
    ret = byval(); //11
    ret = byref(); //11

    ++x;

    ret = byval(); //11
    ret = byref(); //12
}
```


lambda对象不是函数指针，是一个闭包类型的临时对象（右值）
没有捕捉任何变量时，可以转为函数指针