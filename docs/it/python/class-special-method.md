#类特殊方法

##基本操作

###`__new__(cls, *args, **kwargs)`

创建类的实例，必须有返回值，返回实例化出来的实例对象，在__init__之前调用。
用于继承不可变的类时，提供自定义这些类的实例化过程。有时__init__实现不了。

```
class RoundFloat(float):
    def __new__(cls, val):
        return float.__new__(cls, round(val, 2))

f=RoundFloat(1.245)
print(f)


class RoundFloat(float):
    def __new__(cls, val):
        return super(RoundFloat, cls).__new__(cls, round(val, 2))

f=RoundFloat(1.245)
print(f)
```

###`__str__(self)`

输出对象的字符串表示，str和print会调用。

###`__repr__(self)`

被repr函数调用。

###`__unicode__(self)`

被unicode函数调用。

###`__call__(self, *params)`

表示可调用对象。

```
class Test:
    def __call__(self, val):
        return val + 1;

print(Test()(1))
```

###`__bool__(self)`

被bool调用，在需要转换为bool地方被调用。
返回True | False。

```
class Test:
    def __bool__(self):
        print('Test')
        return False

t=Test()
if t:
    print('True')
else:
    print('False')
```

##比较操作

###`__lt__(self, other)`

对应 <。

###`__gt__(self, other)`

对应 >。

###`__le__(self, other)`

对应 <=。

###`__ge__(self, other)`

对应 >=。

###`__eq__(self, other)`

对应 ==。

###`__ne__(self, other)`

对应 !=。

##算术操作

###`__add__(self, other)`

对应 +。

###`__sub__(self, other)`

对应 -。

###`__mul__(self, other)`

对应 *。

###`__truediv__(self, other)`

对应 /。

###`__floordiv__(self, other)`

对应 //。

###`__mod__(self, other)`

对应 %。

###`__divmode__(self, other)`

被divmode函数调用，返回一个元组，包含整除的结果和余数。

###`__pow__(self, other)`

对应 **。

##位操作

###`__lshift__(self, other)`

对应 <<。

###`__rshift__(self, other)`

对应 >>。

###`__and__(self, other)`

对应 &。

###`__or__(self, other)`

对应 |。

###`__xor__(self, other)`

对应 ^。

###`__invert__(self)`

对应 ~。

##一元操作

###`__neg__(self)`

一元负。

###`__pos__(self)`

一元正。

###`__abs__(self)`

被abs函数调用。

##数值转换

###`__complex__(self)`

转换为complex，被complex调用。

###`__int__(self)`

转换为int，被int调用。

###`__float__(self)`

转换为float，被float调用。

###`__oct__(self)`

八进制。

###`__hex__(self)`

十六进制。

##序列操作

###`__len__(self)`

被len函数调用，返回序列的长度。

###`__getitem__(self, item)`

###`__setitem__(self, key, value)`

###`__delitem__(self, key)`

