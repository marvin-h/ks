#原子类型

##atomic

原子操作，就是多线程中最小的不可并行化的操作，意味着在多个线程访问资源时，有且仅有一个线程在对这个资源进行操作

```
#include <atomic>
#include <thread>

using namespace std;

atomic_llong total{ 0 };

void func() {
    for (long long i = 0; i < 1000000; ++i) {
        total += i;
    }
}

int main() {
    thread t1(func);
    thread t2(func);

    t1.join();
    t2.join();

    return 0;
}
```


在`<atomic>`中定义了内置的原子类型
`typedef atomic<long long> atomic_llong;`
`std::atomic<T>`

原子类型不能进行拷贝构造，移动构造，operator=

``` 
atomic<float> af{ 1.1 };
atomic<float> af1{ af }; //error
```

std::atomic<T>定义了到T的类型转换，所以可转为原始类型


##顺序一致性内存模型

原子类型的安全性是建立在顺序一致性模型上的
代码在线程中运行的顺序与看到的代码顺序一致
安全性高，性能弱

```
#include <atomic>
#include <thread>
#include <iostream>

using namespace std;

atomic_int a{ 0 };
atomic_int b{ 0 };

void valueset() {
    int t = 1;
    a = t;
    b = 2;
}

void observe() {
    cout << "a:" << a << endl << "b:" << b << endl;
}

int main() {
    thread t1(valueset);
    thread t2(observe);

    t1.join();
    t2.join();

    cout << "-----------" << endl;
    cout << "a:" << a << endl << "b:" << b << endl;

    return 0;
}
```

线程执行，a和b的结果有可能是：
(0,0)
(1,0)
(1,2)

按顺序执行的理解，(0,2)不应该出现

线程结束后，a和b的结果只能是(1,2)

但是对编译器来说，如果编译器认定a,b赋值语句的执行顺序对输出结果没有任何影响的话，会将指令重排序（reorder）以提高性能

默认情况下，原子类型在线程中总是保持顺序执行

##内存模型

现代处理器不是逐条处理机器指令的

硬件上的内存模型

+ 强顺序内存模型，对于共享内存的处理器，看到内存的数据被改变的顺序与机器指令顺序一样
+ 弱顺序内存模型，可以不一致，具有更高的并行性

在弱顺序内存模型的平台上实现强顺序对性能影响较大

---

c++11内存模型

```
typedef enum memory_order {
    memory_order_relaxed, //不对执行顺序做任何保证
    memory_order_consume, //本线程中，所有后续有关本原子类型的操作，必须在本条原子操作完成后执行
    memory_order_acquire, //本线程中，所有后续的读操作必须在本条原子操作完成后执行
    memory_order_release, //本线程中，所有之前的写操作执行完成后才能执行本条原子操作
    memory_order_acq_rel, // 同时包含memory_order_acquire和memory_order_release
    memory_order_seq_cst //全部存取按顺序执行
    } memory_order;
```

memory_order_seq_cst，默认的原子操作模型

不是所有的atomic成员函数都可以使用所有模型

+   store - memory_order_relaxed / memory_order_release / memory_order_seq_cst
+   load - memory_order_relaxed / memory_order_consume / memory_order_acquire / memory_order_seq_cst
+   RMW（read-modify-write），同时读写的操作可以用所有