#列表初始化

##初始化列表

使用{}初始化

```
int arr[5] = {0};
int arr[] = {1,2,3};
vector<int> v {1,2,3};
map<int,double> m = {{1,1.1}, {2,2.1}};
int i {1};
int i = {1};
int i = {3+4};
double* d = new double {3.3};
```


使用列表初始化还可以防止**类型收窄**，即新类型无法表示原有的类型数据，像精度丢失等

```
char c{ 1024 };//编译器报错
```


##initializer_list

头文件：`<initializer_list>`

想要使用列表初始化，需要声明一个以`initializer_list<T>`为参数的构造函数

例子：

```
#include <initializer_list>
#include <string>
#include <vector>
#include <utility>

using std::initializer_list;
using std::string;
using std::vector;
using std::pair;

enum Gender {male, female};

class People {
public:
    People(initializer_list<pair<string, Gender>> l) {
        for (auto itr = l.begin(); itr < l.end(); ++itr) {
            v.push_back(*itr);
        }
    }

private:
    vector<pair<string, Gender>> v;
};

int main() {
    People p{ {"jim", male }, {"lili", female } };
    return 0;
}
```
