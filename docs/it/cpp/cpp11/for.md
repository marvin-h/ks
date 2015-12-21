#基于范围的for循环

要使用基于范围的for循环，首先要能使用for循环

```
#include <vector>
using std::vector;

int main() {
    int arr[5] = { 3,4,1 };
    for (auto& i : arr) {
        int x = i;
    }

    vector<int> v{ 3,4,1 };
    for (auto e : v) {
        //e代表是容器的对象，不是迭代器
        //auto& e : v，e是引用
    }
}
```