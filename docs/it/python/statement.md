#语句

##代码块

用`:`代表代码块的开始。
用空格或tab缩进语句（推荐4个空格）来创建代码块。
块中每行要有相同的缩进量。


##if

if语句的表达式不需要括号括起来。

```
if expr:
    statements
elif expr:
    statements
else:
    statements
```

```
y = 0
if x < 0:
    y =- 1
elif x < 10:
    y = 0
else:
    y = 1
```

##while循环

```
while expr:
    statements
```

while可与else一起使用，else只在循环结束后执行，break会跳过else。

```
x = 1
while x < 10:
    print(x)
    x += 1


x = 1
while x < 5:
    x += 1
else:
    print(x)
    print('finish')
```


##for循环

```
for var in iterable:
    statements
```

for可与else一起使用，else只在循环结束后执行，break会跳过else。

```
for x in [1,2,3]:
    print(x)


for x in [1,2,3]:
    print(x)
else:
    print('finish')
```


##break

跳出循环。

```
x=1
while x < 100:
    if x > 10:
        break
    x += 1
```

##continue

跳到下一次循环。

##pass

占位，什么也不做。
python不能有空代码块。

```
x = 11
if x > 10:
    pass
```

##assert

断言。

expr为假时，才会触发断言。

```
assert expr[, string]
```

```
x=1
assert x > 0
assert x < 0 #trigger assert
assert x < 0, 'lt 0' #trigger assert
```

##del

移除引用。

```
x = 1
del x
x #error
```


##同一行多个语句

同一行可用`;`分隔语句

```
x=1;x+=2;print(x)
```