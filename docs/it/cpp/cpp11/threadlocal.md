#线程局部存储

TLS，thread local storage

线程局部变量，是拥有线程生命周期及线程可见性的变量

线程有自己的栈空间，但是堆空间和静态数据区是共享的

##thread_local

`int thread_local err;`

thread_local变量，值将在线程开始时被初始化，内存分配是静态的（程序一开始就分配）还是动态的（线程开始时分配），由平台决定。thread_local的性能也有平台决定
