#递归生成器

```
def flatten(nested):
    try:
        try:
            nested+'' #处理字符串
        except TypeError:
            pass
        else:
            raise TypeError
        for sub in nested:
            for e in flatten(sub):
                yield e
    except TypeError:
        yield nested


print(list(flatten([1,[2,[3,4]]])))
#[1, 2, 3, 4]
```