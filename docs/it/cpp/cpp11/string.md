#字符串

##unicode

char16_t，代表utf-16，对应u
char32_t，代表utf-32，对应U

u8 : utf-8
u : utf-16
U : utf-32

```
u8"abc"
u"abc"
U"abc"
```

##原始字符串

没有转义，字符串代表自己
R"(...)"
默认用()，可以换成其他的
R+"+...+"

```
 R"(abc\nnn)" //abc\nnn
```

可以与其他前缀一起使用

```
Ru"(abc)"
```