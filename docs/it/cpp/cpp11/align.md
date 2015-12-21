#对齐

##对齐规则

对齐值必须是2的幂，如果一个类型按n字节对齐，那么该类型的变量的起始地址必须是n的倍数

+   **先按数据自身对齐**

    数据自身的对齐值通常就是数据类型所占的空间大小

+   **再按整个结构体对齐**

    整个结构体的对齐值就是结构体中最大数据类型所占的空间

```
struct Test {
    char c;
    int i;
};// char是1字节，int按4字节对齐，整个结构体就是1+3+4=8

```

```
struct Test {
    int i;
    double d;
    char c;
}; // int补4字节，8+8+1=17，然后按结构体对齐，补齐7个字节等于24

struct Test{
    char c;
    int i;
    double d;
};

// char补齐3个字节，1+3+4+8=16字节
```


##alignof/alignas

`alignof` 查看数据的对齐方式

`alignas` 设置对齐方式

```
struct Test {
    char c;
    int i;
    double d;
};

struct alignas(32) Test1 {
    char c;
    int i;
    double d;
};

int main() {
    int i = alignof(Test); //8
    int i1 = alignof(Test1); //32
}
```

每个平台支持的最大对齐值不一样
可以通过std::max_align_t查询

```
#include <cstddef>
alignof(std::max_align_t);
```