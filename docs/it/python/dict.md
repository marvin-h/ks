#字典

##定义

映射的一种，也可叫关联数组。
字典由键值对组成，由键做索引，键必须为不可变类型，如数字，字符串，只包含数字/字符串的元组。
键必须是可哈希的。
字典是无序的。
用{}表示。

##创建字典

```
{key:val, key1:val1}

dict(mapping) -> new dictionary initialized from a mapping object's 
    (key, value) pairs

dict(iterable) -> new dictionary initialized as if via:
    d = {}
    for k, v in iterable:
    d[k] = v

dict(**kwargs)
```

例子：

```
{'age':18,'name':'jim'}
dict([('name','jim'),('age',18)])
dict(name='jim',age=18)
```

##基本操作

###len(d)

返回元素个数。

###d[k]

返回键为k的值。如果不存在，抛出异常。

###d[k]=v

元素赋值。

###del d[k]

删除键为k的元素。

###k [not] in d

检查是否有键为k的元素，返回True | False。

##方法

###clear()

清空字典。

###copy()

返回浅复制的副本。

```
d={'list':[1,2,3]}
d1=d.copy()
d1['list'][1]=4
print(d) #{'list': [1, 4, 3]}
print(d1) #{'list': [1, 4, 3]}
```

###fromkeys(seq,val=None)

返回一个新字典，以seq的元素为键，val为值。

```
d={}
d1=d.fromkeys([1,2,3],2)
print(d1)
```

###get(key, default=None)

返回键为key的值，如果没找到，返回default。

###items()

返回(key, value)元组的列表。

###keys()

返回键的列表。

###pop(key, default=None)

删除键为key的元素，并返回值，如果没找到，返回default。

###popitem()

随机删除一个元素，返回(key,value)

###setdefault(key, default=None)

如果键不存在，就加上，返回值
如果键存在，设置值，返回值

###update(d)

用另一个字典更新当前字典，如果键相同，值覆盖

###values()

返回值的列表。
