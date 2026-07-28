# 模块与包（Modules and Packages）



## Module（模块）

通常，一个包含 Python 代码的 `.py` 文件就作为一个模块

```text
xxx.py
```

为什么需要模块？例如，一个项目里有 main.py和math_utils.py 两个文件

math_utils.py 里面定义了一些函数：

```python
def add(a,b):
    return a+b


def multiply(a,b):
    return a*b
```

然后 main.py 需要使用这些函数。如果没有模块，可能需要把函数的定义复制到main.py里，重复代码、难以维护、修改麻烦

而使用模块：

```python
import math_utils
```

然后：

```python
math_utils.add(1,2)
```

即可

**import：导入模块**

例如Python内置模块：

```python
import math
```

使用：

```python
math.sqrt(16)
```

结果：

```text
4.0
```

**import的几种方式**

- 方式1（最常见）：import 模块名，导入模块对象，使用时通过模块名访问其中的内容。例如：

```python
import math
```

使用：（需要在前面加模块名）

```python
math.sqrt(16)
```

- 方式2：from 模块 import 内容，导入一个模块的某个内容，例如：

```python
from math import sqrt
```

使用：（不需要在前面加模块名）

```python
sqrt(16)
```

- 方式3（不推荐）：from 模块 import *，导入一个模块的所有内容，例如：

```python
from math import *
```

使用：（不需要在前面加模块名）

```python
sqrt(16)
```

但是不推荐这个方式，因为可能造成名字冲突，例如：

```python
from module1 import *
from module2 import *
```

如果两个模块都有：

```python
test()
```

Python就不知道使用哪个了

**as：给模块取别名**

```python
import 模块 as 别名
```

以后用到这个模块时只需要写别名就行，例如：

```python
import numpy as np
import pandas as pd
```

## Package（包）

- Module：一个 `.py` 文件
- Package：多个模块组成的目录（另外，一个包也可以包含子包），例如：

```text
package/
│
├── __init__.py
├── module1.py
└── module2.py
```

这个目录 package 就是一个包

包和模块的关系：

```text
Package
   |
   ├── Module
   |
   ├── Module
   |
   └── Module
```

大型项目可能有很多个module，通过package把它们组织起来

 **第三方库安装**

例如：

安装 NumPy：

```bash
pip install numpy
```

安装后导入：

```python
import numpy
```

即可使用

~~~text
import 用于导入 Python 模块（module）或包（package）
第三方库（library）通常包含多个包和模块，因此使用第三方库时，本质上也是通过 import 导入其中的包或模块

Library（库）
    ↓
Package（包）
    ↓
Module（模块）
    ↓
Function/Class（函数/类）
~~~

**`__init__.py`**

以前 Python 要求一个目录里必须包含

```text
__init__.py
```

才能被认为是 package。但现在 Python3 中即使没有它也可以作为package

但是实际项目中仍然经常保留，它的作用：

- 在传统意义上用于标识package
- 初始化代码，例如，当import models时执行：

```python
print("models loaded")
```

- 控制导入内容，例如：

```python
from models import *
```

可以控制导入哪些内容

~~~
导入包时，Python 会先根据模块搜索路径找到对应的包目录
如果包中存在 __init__.py 文件，Python 会先执行其中的代码
然后创建对应的包对象
之后就可以通过包名访问其中的模块、变量、函数或类
~~~

**导入路径**

例如：

```
project/

├── main.py
│
└── models/
    ├── __init__.py
    └── model.py
```

那么：

```python
from models.model import Model
```

它的含义：

```
从 models 包
    的 model 模块
        导入 Model 类
```

**requirements.txt**

项目通常需要记录依赖，例如：

```text
numpy==2.0.0
pandas==2.2.0
torch==2.5.0
```

保存为：

```text
requirements.txt
```

拿到项目，执行：

```bash
pip install -r requirements.txt
```

即可安装相同环境

**`__name__ == "__main__"`**

这是 Python 一个非常重要的写法

一个模块既可以单独运行，也可以被其他文件导入

如果它是单独运行的：

~~~python
__name__ == "__main__"
~~~

如果它是被其他文件导入的：

~~~python
__name__ == "这个模块的模块名"
~~~

所以

```python
if __name__ == "__main__"

就等同于

如果 当前文件是直接运行的，而不是被导入的
```