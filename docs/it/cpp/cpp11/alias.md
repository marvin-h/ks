#别名

##typedef (c++98)

`typedef unsigned int unit8;`

##using (c++11)

`using bignum = long long;`

##std::is_same
判断两个类型是否一致

头文件：
`<type_traits>`

例子：
`bool b = std::is_same<bignum, unit8>::value;`

##模板

```
#include <map>
#include <string>

template<typename T> using MapValStr = std::map<T, std::string>;

int main() {
    MapValStr<int> m;
}
```