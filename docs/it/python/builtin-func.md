#内建函数

##print

```
#Prints the values to a stream, or to sys.stdout by default.
#Optional keyword arguments:
    file:  a file-like object (stream); defaults to the current sys.stdout.
    sep:   string inserted between values, default a space.
    end:   string appended after the last value, default a newline.
    flush: whether to forcibly flush the stream.

print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
```

```
print(1,2,3) #1 2 3
print(1,2,3,sep='|') #1|2|3
```

##vars

##locals

返回局部命名空间的字典。

`locals()`

##globals

返回全局命名空间的字典。

`globals()`


##issubclass

##isinstance

##dir

##hasattr

`hasattr(object, name) -> bool`

判断对象是否有该属性。

```
hasattr(foo, '__call__') #是否可调用
```

##getattr

##setattr

##delattr

##abs

`abs(number)`
返回绝对值。
如果是复数，返回math.sqrt(real, imag)

##id

##chr

数字转unicode字符。

`chr(i) -> Unicode character`
Return a Unicode string of one character with ordinal i; 0 <= i <= 0x10ffff.

##ord

ascii字符转数字。

`ord(c) -> integer`

##sorted

```
sorted(iterable, key=None, reverse=False) --> new sorted list
```

返回经过排序后的列表。
key，列表中的每个值会转变为key(val).
reverse，为True时代表逆向排序。

##reversed

```
reversed(sequence) -> reverse iterator over values of the sequence
```

返回经过逆序排序的迭代器对象。

##enumerate

```
enumerate(iterable[, start]) -> iterator for index, value of iterable
```

返回迭代器对象，由索引-值对组成。

```
l=list('hello')
for idx,v in enumerate(l):
 print(idx,v)
```

##zip

```
zip(iter1 [,iter2 [...]]) --> zip object
```

将多个序列压缩在一起，返回一个元组的列表。
不等长的序列，最短序列完了就停止。

```
for v1,v2 in zip(list('ab'),list('bcd')):
 print(v1,v2)
```

###compile

`compile(source, filename, mode[, flags[, dont_inherit]]) -> code object`

生成代码对象。

+   source
    
    源代码。

+   filename

    存放代码对象的文件名。

+   mode

    +   eval, 可求值表达式。
    +   single，单一可执行语句。
    +   exec，可执行语句集合。

```
c=compile('200+300','','eval')
print(eval(c))
```

###eval

`eval(source[, globals[, locals]]) -> value`

对表达式求值。
source可是代码对象，也可以是字符串。
globals，代表全局命名空间，默认是globals()。
locals，代表局部命名空间，默认是locals()。

###exec

执行python语句。
source可是代码对象，也可以是字符串。
globals，代表全局命名空间，默认是globals()。
locals，代表局部命名空间，默认是locals()。


##python3移除的函数

+   coerce
+   apply
+   reduce








