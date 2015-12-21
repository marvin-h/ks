#变长模板

##变长参数

```
#include <stdarg.h>

double sumOfFloat(int count, ...) {
    va_list ap;
    double sum = 0;
    va_start(ap, count);
    for (int i = 0; i < count; ++i) {
        sum += va_arg(ap, double);
    }

    va_end(ap);
    return sum;
}

int main() {
    double s = sumOfFloat(3, 1.1, 2.2, 3.3);
}
```

对于非POD数据类型，变长函数会导致未定义行为

##变长模板

```
template<typname... E> class A;
```

**E叫做模板参数包**
当使用`A<int, char, double>`时，将多个模板参数打包成模板参数包

为了使用模板参数需要**解包**

`template<typename... E> class A:private B<E...>{}`

解包通过**包扩展**，**E...**是一个包扩展

通过递归解包

```
template<typename... E> class Pack;

template<typename Head, typename... Tail>
class Pack<Head, Tail...> : private Pack<Tail...>
{
    Head h;
};

template<> class Pack<> {};


int main()
{
    Pack<int, double> p;
    Pack<int, int, long> p1;
}
```

非模板参数可以用模板参数包

```
template<long... N> struct Multiply;

template<long first, long...last>
struct Multiply<first, last...> {
    static const long val = first*Multiply<last...>::val;
};

template<>
struct Multiply <>{
    static const long val = 1;
};

int main()
{
    long i = Multiply<1, 2, 3>::val;
}
```

##变长模板函数

函数参数包

```
template<typename... T> void f(T... args);
```

函数参数包必须唯一，且是函数的最后一个参数，模板参数包没有这样的要求

##包扩展位置

+   表达式
+   初始化列表
+   基类描述列表
+   类成员初始化列表
+   模板参数列表
+   通用属性列表
+   lambda函数捕捉列表



`A&&...` 可以这样解包，等价于A1&&,...,AN&&

```
template<typename... A> class T: private B<A>... {};
template<typename... A> class T: private B<A...> {};
T<X,Y> t;

//解包为
class T<X,Y> : private B<X>,private B<Y> {};
class T<X,Y> : private B<X,Y> {};
```


##sizeof...

计算参数包中的参数个数

```
template<typename... T> void f(T... args) {
    int i = sizeof...(args);
}

int main() {
    f(1, "ab", 1.1);
}
```


##模板做变长模板的参数包

```
template<typename T> class Vector{};
template<typename T> class List{};

template<typename I, template<typename> class... B> struct Container;

template<typename I, template<typename> class A, template<typename> class... B>
struct Container<I, A, B...> {
    A<I> a;
    Container<I, B...> b;
};

template<typename I> struct Container<I> {};

int main() {
    Container<int, Vector, List> c;
}
```