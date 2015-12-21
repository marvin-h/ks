#auto类型推导

##静态/动态类型

静态类型，需要指定变量类型，类型检查发生在编译期
动态类型，不需要指定变量类型，类型检查发生在运行期

##auto

自动类型推导

```
auto x = 1; //int
auto d = 1.1; //double

#include <map>
#include <string>

using namespace std;

void loop(map<string, string> m) {
    for (auto itr = m.begin(); itr != m.end(); ++itr) {

    }
}
```

##auto使用细则

auto可以和\*/&一起使用
使用指针时，auto*与auto一样
使用引用时，需要用auto&

```
int x = 1;
auto y = &x;
auto* py = &x;
auto& r = x;
```

auto可以和const/volatile一起使用

```
auto x = 1;
x = 2;
const auto y = 1;
y = 2;//编译错误
```

auto可以声明多个变量，但是类型要相同
因为只有第一个变量用于auto的类型推导，然后作用于其他变量

```
auto x = 1, y = 2;
auto z = 1, zz = 2.2;//编译错误
```

##auto使用限制

+ 函数参数
+ 类非静态数据成员
+ 数组
+ 模板实参


```
// 以下都有编译错误

void fun(auto x) {

}

struct str {
    auto x = 1;
};

auto z[3] = { 1 };

vector<auto> v {1};
```
