#std::move

头文件： `<utility>`

将左值强制转化为右值
如果有移动构造函数，调用移动构造函数，否则调用拷贝构造函数

例子：

    #include <utility>

    class Moveable {
    public:
        Moveable():i(new int(0)){}
        Moveable(const Moveable& rhs):i(new int(*rhs.i)) {}
        Moveable(Moveable&& rhs):i(rhs.i) {rhs.i = nullptr;}
        ~Moveable() {delete i;}
    private:
        int* i;
    };

    int main(int argc, char const *argv[])
    {
        Moveable a;
        Moveable c(std::move(a)); 
        //不推荐这样使用
        //对象a还存在，但是i是空指针，不可用。a的生命周期要到main函数结束了才结束
        return 0;
    }


应用：

    #include <utility>
    #include <cstring.h>
    #include <iostream>
    
    using namespace std;
    
    class HugeMem {
    public:
        HugeMem(int size):sz(size>0?size:1){
            p = new int[sz];
            memset(p, 0, sizeof(int)*sz);
    }
    
    HugeMem(const HugeMem& rhs):sz(rhs.sz) {
        p = new int[sz];
        memcpy(p, rhs.p, sizeof(int)*sz);
    }
    
    HugeMem(HugeMem&& rhs):p(rhs.p),sz(rhs.sz){
        rhs.p = nullptr;
        rhs.sz = 0;
    }
    
    ~HugeMem(){delete [] p;}
    private:
        int* p;
        int sz;
    };
    
    class Moveable {
    public:
        Moveable():i(new int(0)), h(1024) {cout<<"default ctr"<<endl;}
        Moveable(const Moveable& rhs):i(new int(*rhs.i)), h(rhs.h) {cout<<"cpy ctr"<<endl;}
        Moveable(Moveable&& rhs):i(rhs.i),
        h(std::move(rhs.h)) // 虽然rhs是右值引用，但是rhs.h是左值
        {
            rhs.i = nullptr;
            cout<<"move ctr"<<endl;
        }
        ~Moveable() {delete i;}
    private:
        int* i;
        HugeMem h;
    };
    
    Moveable getTemp(){
        return Moveable();
    }
    
    int main(int argc, char const *argv[])
    {
        Moveable a(getTemp());
        return 0;
    }

移动语义是为了修改临时变量的值，如果使用常量右值引用就无法修改了
`Moveable(const Moveable&& rhs)`