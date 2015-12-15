#函数

##定义函数

如果函数没有返回值，返回的是None。

语法：

```
def func_name([parameters]):
    statements
```

完整语法：

```
def func_name(positional_params, keyword_params, *tuple_grp_params, **dict_grp_params):
    statements
```

例子：

```
def f(x, y):
    return x + y
```

函数内部可定义函数，叫做内嵌函数。

```
def f():
    def bar():
        print('aa')
    bar()
```

##参数

python函数的参数是对对象的引用，如果在函数中给参数赋值，参数会绑定到另一个对象。

##默认参数

有默认值的参数要放在参数列表的后面。

```
def f(x, y = 1):
    return x + y

f(2)
```

##关键字参数

在标准函数调用中，参数的位置很重要。
关键字参数允许参数缺失或不按顺序，解释器通过关键字来匹配参数。

```
def f(x, y):
    return x + y

ret = f(1,2)
ret = f(y = 2, x = 1) #关键字参数
```

##不定参数

非关键字参数的不定参数：

tuple_grp_params的类型是元组。

```
def func_name(*tuple_grp_params):
    statements
```

关键字参数的不定参数：

dict_grp_params的类型是字典。

```
def func_name(**dict_grp_params):
    statements
```


```
def f(*params):
    for x in params:
        print(x)

def f1(**params):
    for k,v in params.items():
        print(k + ':' + str(v))

f(1,2,3)
f1(x=1,y=2)
```

##参数列表拆分

将列表，元组和字典拆分成函数参数。

`*`拆分列表和元组
`**`拆分字典

```
def f(x, y):
    return x + y

f(*[1,2])
```

##lambda表达式

lambda表达式返回可调用的函数对象

```
lambda [params]: expr
```

```
def f(n):
    return lambda x:x+n
```

##文档字符串

函数，类，模块的最开始的字符串，是对对象用途的总述。
字符串的引号用"。
通过`__doc__`来获得文档字符串。

```
def f():
    "this is a function"
    pass

f.__doc__
```

##函数注释

描述用户自定义函数参数和返回值。
注释以字典的形式存储在`__annotations__`属性中。
参数注释用`:`定义，后加用于计算注释的表达式。
返回值注释用`->`定义，后加用于计算注释的表达式。

```
def f(x:str)->str:
    print(f.__annotations__)
```

