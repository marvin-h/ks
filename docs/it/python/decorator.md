#装饰器

##定义

装饰器是针对函数调用的语法糖。
用于函数或者方法，会产生额外调用。

```
@decorName[(dec_params)]
def func_name([params]):
    statements
```

调用func_name相当于：

```
func_name=decorName(func_name) #装饰器不带参数
func_name=decorName(dec_params)(func_name) #装饰器带参数
func_name()
```

例子：

```
def makebold(fn):
    def wrapped():
        return "<b>" + fn() + "<b>"
    return wrapped

def makeitalic(fn):
    def wrapped():
        return "<i>" + fn() + "<i>"
    return wrapped

@makebold
@makeitalic
def say():
    return "hello world"

say() #"<b><i>hello world<i><b>"
```

##需求

需求，测试性能。

```
import time

def foo():
    print("foo")

start = time.clock()
foo()
end = time.clock()
print('used:', end - start)
```

代码复用，但是改变了调用方式。

```
import time

def foo():
    print("foo")

def timet(fn):
    start = time.clock()
    fn()
    end = time.clock()
    print('used:', end - start)

timet(foo)
```

改进。

```
import time

def foo():
    print("foo")

def timet(fn):
    def wrapper():
        start = time.clock()
        fn()
        end = time.clock()
        print('used:', end - start)

    return wrapper

foo=timet(foo)
foo()
```

语法糖。

```
import time

def timet(fn):
    def wrapper():
        start = time.clock()
        fn()
        end = time.clock()
        print('used:', end - start)

    return wrapper

@timet
def foo():
    print("foo")

foo()
```

##对带参数的函数进行装饰

```
import time

def timet(fn):
    def wrapper(x, y):
        start = time.clock()
        fn(x, y)
        end = time.clock()
        print('used:', end - start)

    return wrapper

@timet
def foo(x, y):
    print(x + y)

foo(3,5)
```


##装饰器带参数

```
import time

def timet(prex):
    def wrapper(fn):
        def wrapped(x, y):
            start = time.clock()
            fn(x, y)
            end = time.clock()
            print(prex + ' used:', end - start)
        return  wrapped
    return  wrapper

@timet('foo')
def foo(x, y):
    print(x + y)

foo(3,5)
```


##装饰器带类参数

```
class locker:
    def __init__(self):
        print("init")

    @staticmethod
    def acquire():
        print("acquire")

    @staticmethod
    def release():
        print("release")

def lock(cls):
    def wrapper(fn):
        def wrapped():
            cls.acquire()
            try:
                return fn()
            finally:
                cls.release()
        return wrapped
    return wrapper

@lock(locker)
def say():
    print("hello world")

say()
```