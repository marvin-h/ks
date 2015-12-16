#元类

##定义

python中的类也是对象，但是这个对象能创建对象。

可以做以下操作：

+   赋值给一个变量
+   拷贝
+   增加属性
+   作为函数参数传递
+   ...

```
def getclass(name):
    if name == 'foo':
        class Foo:
            pass
        return Foo
    else:
        class Bar:
            pass
        return Bar

C=getclass('foo')
c=C()
```

##type

返回对象的类型。
也可以动态创建类。

```
type(object) -> the object's type
type(name, bases, dict) -> a new type
```

```
type(1)
type(int)

newclass=type('Test',(),{})
print(newclass)
```


##元类

元类是类的类，用于创建类，元类实例化的结果就是类。
type就是一个元类，python默认使用的元类。

元类做的事情： 拦截类的创建，修改类，返回修改后的类。

```
type(int)
x=1
x.__class__.__class__
```

##metaclass

metaclass指定了元类。元类不需要正式的类，函数也可以。

先在当前类找metaclass，如果找不到，到父类找，如果找不到，到模块找，如果找不到，就用type。

```
class Foo(metaclass=metaclassname):
    statements

class Foo(Base, Base1, metaclass=metaclassname):
    statements
```

```
class mc(type):
    def __new__(cls, name, bases, attrs):
        print('mc')
        return type.__new__(cls, name, bases, attrs)

class Test(metaclass=mc):
    pass
```

##自定义元类

创建类时其实是调用了type的`__new__`方法分配内存空间，然后调用type的`__init__`方法初始化。自定义元类主要是在`__new__`方法里做文章。

`__new__(cls, name, bases, attrs)`

+   cls，要创建的类
+   name，类名
+   bases，基类
+   attrs，属性

```
def upper_attr(name, bases, attrs):
    attrs = ((n, v)for n, v in attrs.items() if not n.startswith('__'))
    upper_atts = dict((n.upper(), v) for n, v in attrs)
    return type(name, bases, upper_atts)

class upperclass(type):
    def __new__(cls, name, bases, attrs):
        attrs = ((n, v) for n, v in attrs.items() if not n.startswith('__'))
        upper_atts = dict((n.upper(), v) for n, v in attrs)
        return  type.__new__(cls, name, bases, upper_atts)


class Foo(metaclass=upperclass):
    bar = 'cc'

print([name for name in dir(Foo) if not name.startswith('__')])
```