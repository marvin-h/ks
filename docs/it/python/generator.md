#生成器

##定义

生成器是一个带`yield`语句的函数，该函数允许返回值时函数挂起，当调用回到函数时，能够传入改变了的参数，而且从上次离开的地方继续。函数返回值时要用`yield`。
用于创建迭代器。
返回的是一个生成器对象，可以用`next(obj)`调用。

```
def Gen():
    yield 1
    yield 2

for x in Gen():
    print(x)

g=Gen()
print(next(g))
print(next(g))
```

```
def reverse(data):
    for index in range(len(data)-1, -1, -1):
        yield data[index]

for c in reverse('abc'):
    print(c)
```

##方法

###send(val)

向生成器发送值，会成为当前yield的结果。

```
def Gen(n):
    while n >= 0:
        val = (yield n)
        if val is not None:
            n = val
        else:
            n -=1

g=Gen(5)
for n in g:
    print(n)
    if n == 5:
        g.send(3)

# 5 2 1 0
```


###close()

关闭生成器。调用后生成器不再可用。
close是通过在yield表达式中引发一个GeneratorExit异常来实现的。

###throw(type, value, traceback)

在yield表达式中引发一个异常。

##生成器表达式

类似列表推导式，用()，返回一个迭代器。

```
i=(x+2 for x in range(10))
next(i)
```

在函数中可以直接使用，不用额外的括号

```
sum(i*i for i in range(5))