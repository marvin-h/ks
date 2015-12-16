#类

##定义类

语法：

```
class class_name[(base_classes)]:
    body
```

例子：

```
class Test:
    pass
```

类定义要先执行才能生效。
执行类定义会创建一个新的命名空间以及一个类对象。

##类对象

类对象支持两种操作：属性引用和实例化。

属性引用：`className.attr`
实例化：`className()`

```
class Test:
    i = 10
    def f(self):
        return "f"
Test.i
Test.f
t = Test()
```

##构造器

实例化时会调用`__init__(self [,params])`方法，

```
class Test:
    def __init__(self):
        self.name=""

t=Test()
print(t.name)

class Test1:
    def __init(self, name):
        self.name=name

t=Test1('cc')
```

##析构方法

`__del__(self)`

对象的引用为0被GC回收之前做一些清理工作，避免使用


##实例对象

实例化生成的对象。实例对象唯一的操作就是属性引用。

实例对象的属性有两种：

+   数据属性
+   方法

数据属性不需要声明，会在第一次给它们赋值时生成。

方法的第一个参数会绑定到实例对象，一般第一个参数命名为self。方法没有绑定到实例，是不能执行的。

数据属性会覆盖同名的方法属性。

##类变量和实例变量

实例变量属于实例对象。
类变量属于类对象，所有实例对象共享。

```
class Dog:
    t='Dog'
    def __init__(self, name):
        self.name=name

d=Dog('cc')
d1=Dog('dd')
print(d.name)
print(d1.name)
print(d.t)
print(d1.t)
```

##静态方法和类方法

+   静态方法

    用@staticmethod声明，也可以不用声明。
    可以访问类属性，不能访问实例属性。

+   类方法

    用@classmethod声明，有个cls参数。
    可以访问类属性，不能访问实例属性。

+   实例方法

    绑定到实例对象

```
class Test:
    name='cc'
    @staticmethod
    def smethod():
        print('static')
        print(Test.name)

    @classmethod
    def cmethod(cls):
        print('class', cls)
        print(cls.name)

    def imethod(self):
        print('instance')
        print(self.name)
```

##数据隐藏

python没有访问控制，可以通过属性的命名来达到数据隐藏。
在名称前加双下划线`__`，外部不能直接访问，但可以通过`_className+attrName`来访问。

```
class Dog:
    def __init__(self, name):
        self.__name=name

d=Dog('cc')
#print(d.__name)
print(d._Dog__name)
```
