#用户自定义字面量

##字面量操作符
`type operator "" suffix(param)`
""和后缀之间必须有空格
后缀建议以下划线开始

例子：

```
#include <stdlib.h>
#include <iostream>

using namespace std;

typedef unsigned int unit8;

struct RGB
{
    RGB(unit8 r, unit8 g, unit8 b) : r(r), g(g), b(b) {}
    unit8 r;
    unit8 g;
    unit8 b;
};

RGB operator "" _C(const char* col, size_t n) {
    const char* p = col;
    const char* end = col + n;
    const char* r = nullptr;
    const char* g = nullptr;
    const char* b = nullptr;

    for (; p != end; ++p) {
        if (*p == 'r') r = p;
        else if (*p == 'g') g = p;
        else if (*p == 'b') b = p;
    }

    return RGB(atoi(r + 1), atoi(g + 1), atoi(b + 1));
}

long double operator "" _mm(long double l) { return l / 1000; }

int main() {
    RGB color("r1b2g3"_C);
    cout << 1.0_mm << endl;
}
```

##规则
+   如果字面量为整数，字面量操作符的参数只能是unsigned long long或者const char*
    
    当unsigned long long无法容纳字面量时，会将字面量转化为\0结尾的字符串，调用const char* 版本

+   如果字面量为浮点数，操作符参数只能是long double或const char*
+   如果字面量为字符串，操作符参数为const char* 和size_t
+   如果字面量为字符，操作符参数为char