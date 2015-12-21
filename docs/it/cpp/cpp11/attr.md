#通用属性

通用属性用于语言扩展

[[attr]]

##预定义通用属性

[[noreturn]]

用于标示不会返回的函数，不是没有返回值的函数

```
void f1() {
}

void f2() {

}

[[noreturn]] void throwExcep() {
    throw 1;
}

int main() {
    f1();
    throwExcep();
    f2();
}
```

[[carries_dependency]]