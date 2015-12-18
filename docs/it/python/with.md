#with

自动完成清理工作。

```
with contextmgr as newname :
    statements
```

contextmgr，上下文管理器，即支持了`__enter__(self)`和`__exit__(self, exc_type, exc_val, exc_tb)`方法的对象。

`__enter__`，进入with语句块时被调用，返回值绑定在as关键字的变量上。

`__exit__` 有3个参数，异常类型，异常对象和异常回溯。离开语句块时被调用，如果返回false，所有异常不被处理。

```
with open('test.txt') as f:
    print(f.read())
```