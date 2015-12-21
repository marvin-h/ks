#委派构造函数

##定义
构造函数可以调用构造函数，调用者称为委派构造函数，被调用者称为目标构造函数

    class Info
    {
    public:
        Info():l(11)
        {
    
        }
        Info(int i) :Info()
        {
            this->i = i;
    
        }
    
        Info(double d) :Info()
        {
            this->d = d;
        }
    
    private:
        int i = 11;
        double d = 11.1;
        long l;
    };


委派构造函数的初始化列表不能有其他初始化项

    Info(double d) :Info(), i(2) //编译错误
    {
        this->d = d;
    }


委派构造函数可以链式委托，但不能环委托
链式委托：构造函数1委托构造函数2，构造函数2委托构造函数3

##应用
使用构造模板函数生成目标构造函数

    #include <list>
    #include <vector>
    using namespace std;

    class Info
    {
    public:
        Info(const vector<int>& v) :Info(v.begin(), v.end()) {}
    private:
        template<typename T> Info(T first, T second) :l(first, second) {}
        list<int> l;
    };

    int main()
    {
        vector<int> v;
        v.push_back(4);
        v.push_back(2);
        Info c(v);
    }



##异常
目标构造函数发生异常，可以在委派构造函数中捕捉到

    #include <iostream>
    using namespace std;

    class Info
    {
    public:
        Info() { cout << "throw" << endl; throw 1; }
        Info(int i) try :Info() 
        {
            cout << "body" << endl;
        }
        catch (int i)
        {
            cout << "exception" << endl;
        }
    };
    
    int main()
    {
        Info c(1);
    }

输出：

    throw
    exception
    未经处理的异常...
