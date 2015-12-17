#序列

python中的序列：

+   字符串
+   列表
+   元组
+   range

##索引

索引从0开始，最后一个元素的索引可以是-1

```
x='hello'
x[0]
x[-1]
'aa'[0]
```

##连接

`+`实现连接。

```
[1,2]+[3,4] 
```

##重复

`*`实现重复。

```
'ab'*2 # 'abab'
[1,2]*2 # [1,2,1,2]
[None]*10
```


##成员关系操作符

检查一个值是否在序列中

`obj [not] in sequence`

```
'h' in 'hello'
1 in [1,2]
```

##len

通过len函数获得长度

```
len('abc')
```

##切片操作

返回一个子序列。代表前开后闭区间。

`sequence[start : end [: step]]`

step默认为1，不能为0，可以为负。负数代表反向。
step为正数时，start要小于end。
step为负数时，start要大于end。
否则为空序列。

```
x=[1,2,3,4]
x[1:3]
x[:]
x[:2]
x[1:]
x[0:3:2]
x[-2:-1]
```


##range

不可变对象。
类型是range。

```
range(stop) -> range object
range(start, stop[, step]) -> range object
```

```
for x in range(2):
    print(x)
```