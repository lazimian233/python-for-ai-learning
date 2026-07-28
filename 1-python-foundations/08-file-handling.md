# 文件处理（File Handling）



前面学习的变量、列表、函数等，这些数据都存在内存（RAM）中。但是程序关闭之后，内存释放，数据就会消失

所以实际项目中，需要把数据保存到文件里

文件路径（Path）：表示文件的位置

常见的文件类型：

| 类型       | 扩展名  | 用途       |
| ---------- | ------- | ---------- |
| 文本文件   | `.txt`  | 普通文字   |
| Python文件 | `.py`   | Python代码 |
| JSON文件   | `.json` | 数据交换   |
| CSV文件    | `.csv`  | 表格数据   |
| 图片       | `.jpg`  | 图像       |
| 配置文件   | `.yaml` | 配置       |

## open()：打开文件

```python
file = open("文件路径", "模式")
```

例如：

```python
file = open("test.txt", "r")
```

表示：打开 test.txt，打开模式为r（读取）

**常见的文件打开模式**

| 模式 | 英文   | 作用       |
| ---- | ------ | ---------- |
| `r`  | read   | 读取文件   |
| `w`  | write  | 写入文件   |
| `a`  | append | 追加内容   |
| `x`  | create | 创建文件   |
| `b`  | binary | 二进制模式 |

- r模式（读取）

例如：

```python
file = open("test.txt","r")

content = file.read()

print(content)
```

如果文件不存在，会报错：

```text
FileNotFoundError
```

- w模式（写入）

例如：

```python
file = open("test.txt","w")

file.write("hello python")

file.close()
```

注意：这样会覆盖原文件内容

- a模式（追加）

例如：

```python
file = open("test.txt","a")

file.write("\nhello")

file.close()
```

这样就不会覆盖原文件内容，而是在原文件内容后面追加新内容

## close()：关闭文件

```python
file.close()
```

文件属于系统资源，如果不关闭，可能导致：占用资源、文件无法修改、数据没有写入

## with语句

例如：

```python
with open("test.txt","r") as file:

    content = file.read()
```

with语句会自动关闭文件，这样就不用 file.close()了

```text
进入with
 ↓
打开文件
 ↓
执行代码
 ↓
自动关闭文件
```

所以推荐：

```python
with open("test.txt","r") as f:
    data = f.read()
```

## 读取文件

**read()：读取全部内容**

```python
content = f.read()
```

**readline()：读取一行**

```python
line = f.readline()
```

例如，文件：

```text
hello
python
```

第一次结果：

```text
hello
```

第二次结果：

```text
python
```

**readlines()：读取所有行，返回的是列表**

```python
lines = f.readlines()
```

结果：

```python
[
"hello\n",
"python"
]
```

## 遍历文件

文件对象本身可以遍历，例如：

```python
with open("test.txt","r") as f:

    for line in f:
        print(line)
```

适合处理大文件。因为read()会一次性加载全部内容，如果文件过大，可能会占用大量内存

## 写入文件

```python
with open("test.txt","w") as f:

    f.write("hello")
```

注意：`write()`只能写字符串。

## 文件路径

- 相对路径：相对于当前运行目录

例如：

```python
open("data.txt")
```

表示当前目录下的 data.txt

- 绝对路径：从根目录开始的完整路径

Linux：

```python
open("/home/user/data.txt")
```

Windows：

```python
open("C:\\Users\\data.txt")
```

## os模块

Python提供：

```python
import os
```

用于操作系统相关内容

**os.getcwd()：获取当前目录**，例如：

```text
/home/user/project
```

**os.listdir()：查看目录内容**，例如：

返回：

```python
[
"main.py",
"data.txt"
]
```

**os.mkdir()：创建目录**，例如：

```python
os.mkdir("data")
```

创建：

```text
data/
```

**os.remove()：删除文件**，例如：

```python
os.remove("test.txt")
```

## pathlib模块

现代 Python 更推荐：

```python
from pathlib import Path
```

来处理路径。这里导入的Path是一个类

**创建路径对象**

```python
path = Path("data/test.txt")
```

**判断是否存在**

```python
path.exists()
```

**读取**

```python
text = path.read_text()
```

**写入**

```python
path.write_text("hello")
```

## JSON文件

JSON：一种用于数据交换的文本格式，例如：

```json
{
    "name":"Tom",
    "age":20
}
```

**导入**

```python
import json
```

**写入JSON**

```python
data = {
    "name":"Tom",
    "age":20
}


with open("data.json","w") as f:
    json.dump(data,f)
```

**读取JSON**

```python
with open("data.json","r") as f:
    data = json.load(f)
```

结果：

```python
data["name"]
```

得到：

```text
Tom
```

- json.dump()：将 Python 对象（通常是字典）转换为 JSON 格式并写入文件
- json.load()：将 JSON 文件读取并转换为 Python 对象（通常是字典）

## CSV文件

CSV：保存表格数据，每一行是一条数据，用逗号分隔不同列，例如：

```csv
name,age
Tom,20
Bob,21
```

**导入**

```python
import csv
```

**读取CSV**

```python
with open("student.csv") as f:

    reader = csv.reader(f)
```

数据分析阶段，通常使用：

```python
import pandas as pd
```

直接读取csv：

```python
pd.read_csv("data.csv")
```
