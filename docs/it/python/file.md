#文件

python标准换行符是`\n`。
window下，换行符是`\r\n`，所以读文件时`\r\n`会转换为`\n`，写文件时`\n`会转换为`\r\n`。

##操作

###open

```
open(file, mode='r', buffering=-1, encoding=None, 
errors=None, newline=None, closefd=True, opener=None) -> file object
```

返回一个文件对象。

+   file
    文件名。
+   mode

    +   'r'
        open for reading (default)
    +   'w'
        open for writing, truncating the file first
    +   'x'
        create a new file and open it for writing
    +   'a'
        open for writing, appending to the end of the file if it exists
    +   'b'
        binary mode
    +   't'
        text mode (default)
    +   '+'
        open a disk file for updating (reading and writing)
    +   'U' 
        在读文件时，使用统一的行分隔符。编译python时，默认是打开的。

+   buffering

    + 0/False，无缓冲
    + 1/True，有缓冲
    + -1，使用默认缓冲区大小
    + 大于1，缓冲区大小

###write(s)

写文件。

###read(n)

读多少个字节，如果忽略参数，全读。

###close()

关闭文件。
使用文件后要关闭，可以用try/finally，也可以用with。

```
f=None
try:
    f=open('test.txt','r')
    print(f.read())

finally:
    f.close()

with open('test.txt') as f:
    print(f.read())
```

###seek(offset[,whence])

把当前位置移到指定位置。

offset，偏移量。

whence

+   0
    从文件开头计算偏移量，默认值。
+   1
    从当前位置计算偏移量。
+   2
    从文件结尾计算偏移量，offset此时为负。

###readline(limit)

读取一行，limit代表读取的最大字节数。

###readlines()

读取所有行，返回列表。

###flush()

刷新缓冲区。

###tell()

返回文件的位置。

