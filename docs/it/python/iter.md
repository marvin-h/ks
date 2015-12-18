#迭代器

##定义

实现遍历功能。

对象要实现迭代功能，要实现`__iter__()`和`__next__()`方法。
`__iter__()`返回一个迭代器对象，迭代器对象是具有`__next__()`方法的对象。
`__next__()`方法会返回下一个元素，如果没有后续元素，返回`StopIteration`异常。

for语句会调用`iter(obj)`函数，该函数调用对象的`__iter__()`方法。当抛出`StopIteration`异常，for循环终止。

内建函数`next(obj)`会调用`__next()__`方法。

```
s='abc'
i=iter(s)
next(i)
next(i)
next(i)
next(i)
```

```
class MyIterObj:
    def __init__(self, start, end):
        self.val = start
        self.end = end

    def __iter__(self):
        return  self

    def __next__(self):
        if self.val >= self.end:
            raise  StopIteration
        ret = self.val;
        self.val += 1
        return ret

o = MyIterObj(1,5)
for x in o:
    print(x)
```