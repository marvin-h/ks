#非受限联合体

c++98中对联合体有很多限制，c++11废除了一些限制

```
#include <string>
using std::string;
union T {
    string s;//非POD类型，c++98编译失败
    int i;
};
```

c++11允许联合体中有非POD数据成员，但是该成员如果有non trivial构造函数，默认构造函数将被编译器删除。其他特殊成员函数，如默认拷贝构造函数，默认拷贝赋值操作符等也遵守此规则

```
int main() {
    T t;//编译失败，s的默认构造函数被删除
}
```

解决办法，为非受限联合体定义构造函数
```
union T {
    string s;
    int i;
public:
    T() { new (&s) string; }
    ~T() { s.~string(); }
};
```

##匿名非受限联合体运用在类中

```
struct Student {
    Student(bool g, int a) : gender(g), age(a) {
    }
    bool gender;
    int age;
};

class Singer {
public:
    Singer(bool g, int a):s(g, a) {}
    Singer(int i) : id(i) {}

private:
    union {
        Student s;
        int id;
    };
};

int main() {
    Singer s(true, 19);
    Singer s1(11);
}
```