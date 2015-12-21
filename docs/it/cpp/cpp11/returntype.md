#返回类型追踪

一般用于模板，模板实例化时自动推导返回类型

```
template<typename T1, typename T2>
auto Sum(const T1& t1, const T2& t2) ->decltype(t1 + t2) {
    return t1 + t2;
}

int main() {
    auto i = Sum(1, 1.2);
}
```

```
//auto (*)() -> int(*)() 返回函数指针的函数，设为a
//返回a函数的指针的函数
auto pf1() -> auto (*)()->int(*)() {
    return nullptr;
}
```

```
int (*fp)();
等价于
auto (*fp)() ->int;
```