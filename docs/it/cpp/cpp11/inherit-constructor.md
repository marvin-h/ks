#继承构造函数

##继承构造函数
c++11之前需要显示调用基类构造函数

    class A
    {
    public:
        A(int) {}
        A(double, int) {}
    
        virtual ~A() {}
    };

    class B : public A
    {
    public:
        B(int i):A(i) {}
        B(double d, int i):A(d, i) {}
    };

    int main()
    {
        B b(1,1);
    }


C++11的继承构造函数
使用using

    class A
    {
    public:
        A(int) {}
        A(double, int) {}

        virtual ~A() {}
    };

    class B : public A
    {
    public:
        using A::A;
    };


    int main()
    {
        B b(1,1);
    }

如果继承构造函数不被相关代码使用，是不会生成函数代码的
基类的构造函数是私有的或者派生类是虚继承，不能使用继承构造函数
一旦使用了继承构造函数，编译器就不会为派生类生成默认构造函数

##基类的构造函数有默认值
参数的默认值是不会被继承的

    class A
    {
    public:
        A(double d = 2.0, int i = 1) {}

        virtual ~A() {}
    };

    class B : public A
    {
    public:
        using A::A;
    };

类A可能的构造函数

+ A()
+ A(double d)
+ A(double d, int i)
+ A(const A&)

类B也有相应的构造函数


