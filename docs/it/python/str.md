#字符串

##定义

序列的一种。
类型是str。
字符串是不可变类型，改变字符串的元素需要新建一个字符串。
用单引号或双引号表示字符串。
字符串中`\`代表转义。

```
'hello'
"hello"
s = 'cc'
s = str(1)
```

##更新元素

不能给字符串的元素赋值。

```
s ='hello'
s[0] = 'c' # error
s = 'c' + s[1:]
s = 'world'
```

##序列操作

[序列操作](sequence.md)

##格式化

`format_string % values`

values如果是元组或者字典，可以匹配多个值。列表只能匹配一个值。

```
'hello %s' % 'jim'
s = 'hello %s and %s'
s % ('jim', 'lili')

'hello %(name)s and %(name1)s' % {'name1' : 'jim', 'name' : 'lili'}
```

格式化字符：

+   **%s**，优先用str转换
+   **%r**，优先用repr转换
+   **%d / %i / %u**，转成有符号十进制数
+   **%o**，转成八进制数
+   **%x**，转成十六进制数
+   **%f**，转成浮点数
+   **%e**，转成科学计数法
+   **%%**，输出%

格式顺序：

+ **%**
+ **转换标志**

    + **-**，左对齐
    + **+**，转换前要加正负号
    + **空格**，正数之前保留空格
    + **0**，位数不够用0填充
    
+ **最小字段宽度**

    字符串至少应该具有该值的宽度，如果是\*，宽度从元组读出

+ **.后跟精度值**
    
    如果是实数，精度值代表小数点后的位数，如果是字符串，代表最大宽度，精度值如果是\*，宽度从元组读出

+ **转换类型**

    对应格式化字符


##模板字符串

```
from string import Template
Template('$x, hello $x')
s.substitute(x='mm') # 'mm, hello mm'

s=Template('$thing, happy $done')
d={}
d['thing']='jim'
d['done']='lili'
s.substitute(d) # 'jim, happy lili'
```

##原始字符串

以`r`开头的字符串是原始字符串

原始字符串不能以\\结尾

```
r'a\\b' # 'a\\\\b'
```


##方法

###capitalize()

第一个字符大写。

```
s = 'hello'
s.capitalize()
```

###center(width, fillchar = ' ')

将字符串扩充至width长度，不够的地方补fillchar。字符串居中。
如果字符串长度超过width，不做任何操作。

###count(sub, start=0, end=len(string))

返回sub在string里出现的次数。可以指定范围。

###encode(encoding='utf-8', errors='strict')

按指定编码格式编码。

###find(sub, start=0, end=len(string))

检测sub是否包含在string中，可以指定范围。
如果找到，返回开始索引，否则返回-1.

###index(sub, start=0, end=len(string))

和find一样，但是如果sub不在string中，会抛出异常。

###join(iterable)

以string为分隔符，将iterable的元素拼接，合并成新字符串。

```
' '.join('abc')
```


###replace(old, new, count=string.count(old))

将old字符串替换成new，替换次数不超过count。

###startswith(prex, start=0, end=len(string))

检测字符串是否以prex开头。返回True | False。

###split(sep='', maxsplit=string.count(sep))

以sep为分隔符切片string。最多切maxsplit次。返回列表。

```
s='aabcc'
s.spilt('b')
```

