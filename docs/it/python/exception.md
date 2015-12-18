#异常

`Exception`是所有异常的基类。异常一般会定义`__str__()`函数。

##捕捉异常

`try/except`

```
def div(x,y):
 try:
  return x/y
 except ZeroDivisionError:
  print('div zero error')
 except TypeError:
  raise


def div(x,y):
 try:
  return x/y
 except (ZeroDivisionError, TypeError):
  print('...')


def div(x,y):
 try:
  return x/y
 except (ZeroDivisionError, TypeError) as e:
  print(e)

#全捕捉
def div(x,y):
 try:
  return x/y
 except:
  print('error')
```

---

`try/except/else`

没有异常时执行else

```
def div(x,y):
 try:
  r=x/y
 except:
  print('div zero')
 else:
  print('ok')
  return r
```

---

`try/except/finally`

不管是否引发异常，finally都会执行。

```
try:
    x=1/0
finally:
    print('div zero')
```

##引发异常

```
# exception可以是异常类或者异常实例。
raise exception
```

```
# 重新抛出异常
raise
```

##自定义异常

```
class MyException(Exception):
    statements
```