#基础

##源文件

源文件以py为扩展名。

```
hello.py
```

##help

help(func | class | module)

查看函数，类，模块的帮助文档。

```
help(int)
```

##注释

注释行以#开头。

```
#this is note
```

##标识符

标识符名可由字母，数字，下划线组成。不能以数字开头。
同时以双下划线开头和结尾的标识符有特殊含义，不要随意使用。如`__future__`，`__init__`等

##变量

python的变量是对对象的引用。
必须对变量初始化，初始化就是将变量绑定到对象。

```
x=1
y_1='aa'
```

##输入

`input`

```
x=input('name:')
```

##输出

`print`

```
print('hello world')
```