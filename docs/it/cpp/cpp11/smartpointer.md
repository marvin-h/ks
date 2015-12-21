#智能指针

头文件：

`<memory>`

##unique_ptr

唯一所有权，不能赋值，但可以用move转移所有权

```
#include <memory>

using namespace std;

int main() {
    unique_ptr<int> p(new int(11));
    unique_ptr<int> p1 = move(p);
    unique_ptr<int> p2 = p1; //编译错误
}
```

##shared_ptr

共享所有权

```
#include <memory>

using namespace std;

int main() {
    shared_ptr<int> p(new int{ 1 });
    shared_ptr<int> p1 = p;
}
```

##weak_ptr

