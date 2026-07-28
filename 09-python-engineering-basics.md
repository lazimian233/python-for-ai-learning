# Python工程基础（Python Engineering Basics）



## 环境管理

- pip：Python包管理器

见Linux笔记02-package-management

- venv：Python虚拟环境工具

见Linux笔记02-package-management

- requirements.txt记录依赖

见Python笔记01-python-environment

## 项目组织

一个简单项目：

```text
my_project/

├── main.py
├── utils.py
├── config.py
└── requirements.txt
```

一个大型项目：

```text
my_project/

├── main.py

├── models/
│   ├── __init__.py
│   └── model.py

├── datasets/
│   ├── __init__.py
│   └── dataset.py

├── utils/
│   ├── __init__.py
│   └── tools.py

├── configs/
│   └── config.py

├── requirements.txt

└── README.md
```

| 目录     | 作用     |
| -------- | -------- |
| models   | 模型代码 |
| datasets | 数据处理 |
| utils    | 工具函数 |
| configs  | 配置文件 |

**.gitignore：忽略不需要提交的文件**

导入模块时可能会生成一个目录：

```text
__pycache__/
```

里面大概是这样的文件：

```text
module.cpython-xxx.pyc
```

这是Python字节码文件，用于提高模块加载速度，一般忽略：

```text
__pycache__/
*.pyc
```

另外，这些也可能忽略：

```text
data/
checkpoints/
logs/
```

## 代码规范

Python官方推荐规范：PEP 8

**命名规范**

变量和函数像这样：snake_case

类像这样：PascalCase

常量像这样：MAX_SIZE

**代码格式**

缩进空4个空格

函数之间空两行

```python
def func1():
    pass


def func2():
    pass
```

## 工程工具

**类型提示（Type Hint）**

Python是动态类型语言，类型可以变动，但是大型项目中还是需要增加类型提示

例如，普通情况下：

```python
def add(a,b):
    return a+b
```

增加类型提示：

```python
def add(a: int, b: int) -> int:
    return a+b
```

表示：传入的两个参数都是int类型，返回的结果也是int类型

**日志（Logging）**

程序运行时需要记录信息，例如训练模型：

```text
Epoch 1 loss=0.5
Epoch 2 loss=0.3
```

这就是日志

Python提供

```python
import logging
```

简单使用：

```python
import logging

logging.info("training start")
```

日志级别：

| 级别     | 作用     |
| -------- | -------- |
| DEBUG    | 调试信息 |
| INFO     | 普通信息 |
| WARNING  | 警告     |
| ERROR    | 错误     |
| CRITICAL | 严重错误 |

**调试（Debug）**

程序出错时需要定位问题

最简单的方式，打印变量：

```python
print()
```

或者Python调试器：

```python
pdb
```

或者 IDE：VS Code、PyCharm等

它们提供：

- 断点
- 单步执行
- 查看变量

**异常处理（Exception Handling）**

程序运行可能出错

例如：运行到x = 10 / 0会报错：ZeroDivisionError

异常处理的格式：

```python
try:
    可能出错代码

except:
    错误处理
```

例如：

```python
try:
    x = 10 / 0

except ZeroDivisionError:
    print("error")
```

```python
try:
    with open("data.txt") as f:
        data=f.read()

except FileNotFoundError:
    print("file not found")
```
