#显式类型转换操作符

##explicit用于构造函数
explicit用于构造函数，表示禁止隐式构造，必须显式构造

```
class A {
public:
    explicit A(int i, double d = 0) : m_i(i), m_d(d){}

private:
    int m_i;
    double m_d;
};


int main()
{
    A a = 1;//error
    A a = A(1);
}
```


##显式类型转换
c++11中，explicit可以用于类型转换操作符

```
class ConvertTo {};

class Convertable {
public:
    explicit operator ConvertTo () const {
        return ConvertTo();
    }
};


int main()
{
    Convertable c;
    ConvertTo t(c);
    ConvertTo t2 = c;//拷贝构造被禁止
    ConvertTo t3 = static_cast<ConvertTo>(c);
}
```