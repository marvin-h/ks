#继承

##定义

基类和派生类要在同一个命名空间。
python自定义类都继承object。

语法：

```
class class_name(base_class_name):
    statements
```

```
class Base:
    def __init__(self, name):
        self.name = name

class D(Base):
    def __init__(self, name, age):
        super(D, self).__init__(name)
        self.age=age
```

##多重继承

语法：

```
class class_name(base_class_name1, base_class_name2):
    statements
```

##方法搜索

python中的方法都是虚的。
方法的查找是先搜索当前类，再沿基类链逐级搜索。
多重继承时从左到右广度优先搜索，先搜索直接基类，再逐级搜索。

```
class Base:
    name='base'

class A1(Base):
    pass

class A2(Base):
    name='a2'

class B(A1, A2):
    pass

print(B.name) #a2
```

##调用基类同名方法

两种方式：

+   BaseClass.method(self, params)

    一般不用

+   super(DerivedClass, self).method(params)

```
class Test:
    def __init__(self, value):
        self.name=value
        
class Child(Test):
    def __init__(self, value):
        Test.__init__(self, value)
```

```
class Test:
    def __init__(self, value):
        self.name=value
        
class Child(Test):
    def __init__(self, value):
        super(Child, self).__init__(value)
```

##super

`super(type[,obj])`

查找父类，返回type的父类。
如果父类需要被绑定，可以传入obj。obj也可以是一类型，必须是type的子类。

如果obj是一个实例，isinstance(obj, type)必须返回True。
如果obj是一个类，issubclass(obj, type)必须返回True。


