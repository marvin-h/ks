#默认函数控制

**类的默认函数**

+ 构造函数
+ 拷贝构造函数
+ 移动构造函数
+ 拷贝赋值函数
+ 移动赋值函数
+ 析构函数

**类的全局默认操作符**

+ `operator,`
+ `operator&`
+ `operator&&`
+ `operator*`
+ `operator->`
+ `operator->*`
+ `operator new`
+ `operator delete`

如果没有定义，编译器会自动生成


##default

显式指定编译器生成默认版本的函数

`=default`修饰的函数叫显式默认函数

```
#include <type_traits>

using namespace std;

struct A {
    A() {}
};

struct B {
    B() = default;
};

int main() {
    bool a = is_pod<A>::value; //false
    bool b = is_pod<B>::value; //true
}
```


##delete

指示编译器不生成默认版本的函数
删除不该让用户使用的函数

`=delete`修饰的函数叫删除函数

```
#include <type_traits>

using namespace std;

struct A {
    A() {}
    A(const A& rhs) = delete;
};


int main() {
    A a;
    A a1(a); //error
}
```

`=delete`可以用在普通函数

```
void f(int) {}

void f(char c) = delete;

int main() {
    f(1);
    f('c'); //error
}
```

避免堆上分配对象

```
#include <cstddef>

struct A {
    void* operator new(std::size_t) = delete;
};


int main() {
    A a;
    A* p = new A; //error
}
```

在指定内存位置分配的对象，不需要析构函数来清理对象

```
#include <new>

struct A{
    ~A() = delete;
};

int main() {
    A a; //error
    char* p = new char[1024];
    A* pa = new (p) A;
}
```