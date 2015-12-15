#运算符

##运算符

规则：

+   如果有一个操作数复数，另一个操作数先转换为复数。
+   否则，如果有一个操作数是浮点数，另一个操作数先转换为浮点数。
+   否则，如果有一个操作数是长整数，另一个操作数先转换为长整数。
+   否则，两者都是普通整数，无需转换。

##算术运算符

```
+
-
*
/
%
** 幂
// 整除，舍去小数部分
```

```
3+2
3-2
3*2
3/2 #1.5
3%2
3**2 #9
3//2 #1
```

##关系运算符

```
<
>
<=
>=
==
!=
is #指向同一个对象
is not
in #判断元素是不是在序列中
not in
```

python允许`2 < x < 3`。
避免将`is`用于数值或字符串等不可变值。

```
x=[1]
y=[1,2]
x is y
```

##逻辑运算符

```
and
or
not
```

##条件运算符

python没有`expr?expr1:expr2`这种条件运算符。

格式：

`expr if expr1 else expr2`

```
x=1
y=2
x if x>y else y
```

##位运算符

```
& 按位与
| 按位或
~ 按位取反
^ 按位异或
<< 左移
>> 右移
```