#强类型枚举

##c++98的枚举

c++98的枚举类型及成员会污染命名空间

```
namespace NS {
    enum Type {male, female};
    enum Gender {male, female};
}

int main() {
    using namespace NS;
    Type t = Type::female;
    if (t == male) { //不知道是哪个male，编译错误

    }
}
```

c++98的枚举会隐式提升为整型，容易造成错误

枚举类型所占用的空间也不确定，会根据枚举成员的值改变

##强类型枚举

`enum class Gender {male, female};`

优点：

+ 不会污染命名空间
+ 不能隐式转换为整型
+ 可以指定底层类型

```
enum class Gender:char {male, female};
Type t = male; //编译错误
Type t = Gender::male;
```
