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

##getattr

##setattr

##delattr

##abs(number)

返回绝对值。
如果是复数，返回math.sqrt(real, imag)

##id

##chr(i)

数字转unicode字符。

chr(i) -> Unicode character
Return a Unicode string of one character with ordinal i; 0 <= i <= 0x10ffff.

##ord(c)

ascii字符转数字。

ord(c) -> integer

##sorted

##reversed

##enumerate

##zip

##python3移除的函数

+   coerce
+   apply
+   reduce








