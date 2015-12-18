#集合

##定义

集合中的元素不会重复且没有顺序。
集合是可变的，但是元素必须是不可变的。
集合的元素必须是可哈希的。
类型是set。
用{}表示。

```
{1,2,2} #{1,2}
```

空集合必须用`set()`创建。


##frozenset

不可变集合，不能增加删除元素。

```
s=set([1,2,1])
s.add(set([1])) # error
s.add(frozenset([1]))
```

##基本操作

###len(s)

返回元素的个数。

###[not] in

元素是否在集合中。


##方法

###issubset(s)

是否是s的子集
可以用<=
< 真子集

```
a=set([1,2])
b=set([2,3])
a.issubset(b)
a<=b
```

###issuperset(s)

是否是s的超集
可以用>=

```
a=set([1,2])
b=set([2,3])
a.issuperset(b)
a<=b
```

###union(s)

合并，可用|

```
a.union(b)
a|b
```

###intersection(s)

交集，可以&

```
a.intersection(b)
a&b
```


###difference(s)

差，可以-

```
a.difference(b)
a-b
```

###symmetric_difference(s)

对称差，可以^
在a中不在b中或在b中不在a中


###update(s)

更新当前set，可用|=

```
s=set()
s1=set([1,2])
s.update(s1)
s|=s1
```

###intersection_update(s)

只保留交集部分，可用&=


###difference_update(s)

可用-=

###symmetric_difference_update(s)

可用^=

###add(x)

增加元素。

###remove(x)

删除元素，如果不存在会抛出异常。

```
s={1,2}
s.remove(1)
```

###pop(x)

删除并返回元素。

###clear()

清空集合。

###discard(x)

删除元素，元素不存在不会抛出异常。



