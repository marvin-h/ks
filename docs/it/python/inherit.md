#继承

##定义

基类和派生类要在同一个命名空间。

语法：

```
class class_name(base_class_name):
    statements
```

##多重继承

语法：

```
class class_name(base_class_name1, base_class_name2):
    statements
```

##方法搜索

方法的查找是先搜索当前类，再沿基类链逐级搜索。
python中的方法都是虚的。
多重继承时从左到右深度优先搜索，优先使用先继承的方法。

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
