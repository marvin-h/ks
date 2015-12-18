#with

自动完成清理工作。

```
with contextmgr as newname :
    statements
```

contextmgr，上下文管理器，即支持了`__enter__`和`__exit__`方法的对象。

```
with open('test.txt') as f:
    print(f.read())
```

##方法

`__enter__(self)`

进入with语句块时被调用，返回值绑定在as关键字的变量上。

`__exit__(self, exc_type, exc_val, exc_tb)` 

有3个参数，异常类型，异常对象和异常回溯。
在with代码块中引发的异常，会传入`__exit__`，如果没有异常，3个参数都是None。
`__exit__`在离开with代码块时被调用，可以在此处理with代码块引发的异常，如果返回False，异常会再次抛出，如果返回True，异常不会再次抛出。

```
class Mywith:
    def __enter__(self):
        print('enter')

    def __exit__(self, exc_type, exc_val, exc_tb):
        print('exit')
        return True

with Mywith() as m:
    print('...')
    raise Exception('e')
```
