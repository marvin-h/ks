#右值引用

##左值 右值

+ 左值，可以取地址，有名字
+ 右值，不能取地址，没有名字

例子：

    a = b + c; //a是左值，b+c是右值


##左值引用 右值引用

+ 左值引用， T& a
+ 右值引用， T&& a

引用必须立即初始化，无论左值引用还是右值引用

右值引用不能绑定到左值
左值引用不能绑定到右值，但常量左值引用可以，常量左值引用是万能引用
右值一旦绑定到引用，生命周期就延长了

例子：

    int&& a = 1;
    int b = 10;
    int&& c = b; //error

    int& d = 1; //error
    const int& e = 1;

    //const lvalue ref
    void test(int& i) {}

    void test1(const int& i) {}

    int ret() {
        return 10;
    }

    test(ret());//error
    test1(ret());


##常量右值引用

const T&& a
常量右值引用一般没有什么作用
