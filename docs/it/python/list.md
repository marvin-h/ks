#列表

##定义

序列的一种。
类型是list。
用[]表示。类似数组。
列表的元素可以是不同类型。

```
[1,2,3]
[1, 'a']
l=list('abc')
```


##序列操作

[序列操作](sequence.md)

##更新元素

```
l=[1,2,3]
l[0] = 2
```

##删除元素

```
del list[i]
del list[start:end]
```

```
l=[1,2,3]
del l[0]
```

##切片赋值

```
x=list('perl')
x[2:]=list('ar')

#插入
x=[1,5]
x[1:1]=[2,3,4] #[1,2,3,4,5]

#删除
x[1:4]=[]
```


##方法

###append(obj)

在末尾追加新对象。

###count(obj)

返回obj出现的次数。

###extend(sequence)

在末尾追加序列。

###index(obj, start=0, end=len(list))

返回obj的索引，如果没找到，抛出异常。

###insert(i, obj)

在索引为i的地方插入obj。

###pop(i=-1)

删除并返回指定位置的对象。默认是最后一个对象。

###remove(obj)

删除第一个匹配的元素。没找到会抛出异常。

###reverse()

逆向排序。

###sort(func=None, key=None, reverse=False)

以指定方式排序。
func，排序算法。
key，列表中的每个值会转变为key(val).
reverse，为True时代表逆向排序。

```
l=['321','2421','32']
x=l[:]
x.sort() 
y=l[:]
y.sort(reverse=True)
z=l[:]
z.sort(key=int)

#['2421', '32', '321']
#['321', '32', '2421']
#['32', '321', '2421']
```


##列表解析

提供了一个生成列表的简洁方法。

```
[x*x for x in range(3)]
[x*x for x in range(3) if x%3==0]
[(x,y) for x in range(3) for y in range(3)]
```