#模块

##定义

模块是python代码的逻辑上的组织形式，物理形式是文件。
模块名就是python文件名去掉扩展名。

##使用模块

一个模块只会被加载一次，无论被导入多少次。

方式一：

这种方式使用时要加上模块名作为前缀。

```
import modulename1 [as newname] [,modulename2 [as newname]]
```

```
import sys, socket
print(sys.argv[0])

import math as m
```

方式二：

这种方式不需要前缀。

```
from module import attr [as newname] [,attr1 [as newname]]
from module import *
```


```
from math import sqrt
print(sqrt(2))
```


##模块查找

查找顺序：

+   脚本所在的目录
+   PYTHONPATH变量

可通过sys.path查看和增加查找路径。

```
import sys
sys.path.append('/tmp/test')
```


##编译后的python文件

为了加快模块的加载速度，python会在`__pycache__`目录下以module.version.pyc名字缓存每个模块编译后的版本。

通过检查源文件和编译版本的修改日期确定是否要重新编译。

两种情况不检查缓存：

+   总是重新编译且不存储从命令行加载的模块
+   模块只有编译后的版本且没有源文件


##包

也是模块的一种，对应的是目录。

目录下必须包含名为`__init__.py`的文件。可以是空文件。为包执行初始化代码。

```
import package
import package.module
from package import module
```

##属性隐藏

以双下划线开头的命名不能直接引用。

##`__all__`

如果`__init__.py`中定义了一个名为`__all__`的列表，遇到`from package import *`，只会导入列表的模块。
如果没有定义，不会导入所有子模块，只会导入包定义的名称，即`__init__.py`中定义的名称（包括它显示导入的名称）。

##`__import__`


##查看模块信息

```
dir(package)
[n for n in dir(mypackage) if not n.startswith('__')]

help(package)

package.__file__ # 源代码位置
```
