#常量表达式

constexpr

##运行时常量

```
const int getcount() {return 1;}
int arr[getcount()]; //编译错误
```

##编译时常量

```
constexpr int getcount() { return 1; }
int arr[getcount()];
```

##常量表达式函数

+ 只能有单一的return语句，不会实际产生代码的语句，如static_assert则没关系
+ 必须返回值
+ 使用前必须有定义
+ return语句中不能使用非常量表达式函数

```
constexpr int getcount() { static_assert (true,"aa");  return 1; }
constexpr int get() {return getcount();}
```


##常量表达式值

```
const int i = 0;
constexpr int j = 0;
```

如果i和j位于全局空间，编译器会为i产生数据，对于j，如果没有代码用到，不会产生数据

标准要求编译期常量浮点数在编译时的精度要大于等于运行时

##模板

常量表达式可以用于模板函数返回值，如果实例化时不满足常量表达式，会忽略constexpr

```
template<typename T> constexpr T get(T t) { return t; }
struct  MyType {};
int main() {
    MyType t;
    MyType t1 = get(t);
    constexpr int i = get(1);
}
```

##递归

编译期计算
标准要求至少支持512层递归

```
constexpr int fib(int n) {
    return (n == 1) ? 1 : ((n == 2) ? 1 : fib(n - 1) + fib(n - 2));
}

int main() {
    int fibarr[] = { fib(11), fib(12), fib(13), fib(14) };
}
```

模板元编程，基于模板的编译时期运算的编程方式

```
template<long num>
struct Fib
{
    static const long val = Fib<num - 1>::val + Fib<num - 2>::val;
};

template<> struct Fib<2>
{
    static const long val = 1;
};

template<> struct Fib<1>
{
    static const long val = 1;
};

template<> struct Fib<0>
{
    static const long val = 0;
};

int main() {
    int fib[] = { Fib<11>::val, Fib<12>::val };
}
```