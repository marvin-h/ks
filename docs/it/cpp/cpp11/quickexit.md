#程序退出

##terminate

调用terminate的情况

+ 没有被捕捉的异常
+ noexcept函数抛出异常

默认情况下，terminate会调用abort
可以用set_terminate来改变默认行为

##abort

异常终止
abort比terminate更底层，不会调用任何析构函数。abort有时候会带来一些问题，如果与其他进程交互，可能会导致这些进程处于中间状态

##exit

正常退出，会调用变量的析构函数。还会调用atexit注册的函数，调用顺序与注册顺序相反


```
#include <iostream>

using namespace std;

void opendev() {
    cout << "device opened" << endl;
}

void closedev() {
    cout << "device closed" << endl;
}

void releasedev() {
    cout << "device release" << endl;
}

int main() {
    atexit(closedev);
    atexit(releasedev);
    opendev();
    exit(0);
}
```

##quick_exit

exit函数在结束时会调用类的析构函数，并将零散内存还给操作系统，这比较耗时。操作系统回收内存只是将物理内存标记为未使用，很多时候调用析构函数是无意义的

在多线程情况下，使用exit来退出程序，通常需要向线程发送一个信号，等待线程结束后再执行析构函数和atexit注册的函数，不过有时候不能像预期那样工作。如线程在等待IO运行结束，因为信号问题导致的死锁等。程序会卡死而无法退出。

quick_exit不调用析构函数只是是程序终止，但是是正常终止。可以用at_quick_exit来注册清理函数

