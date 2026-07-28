# Python环境（Python Environment）



**什么是 Python**

Python 是一种：

- 高级语言（High-level Language）
- 解释型语言（Interpreted Language）
- 通用编程语言（General-purpose Programming Language）

它的特点：

- 简洁
- 丰富的生态，例如：

| 领域     | Python库     |
| -------- | ------------ |
| 数学计算 | NumPy        |
| 数据分析 | Pandas       |
| 机器学习 | Scikit-learn |
| 深度学习 | PyTorch      |
| 可视化   | Matplotlib   |

**Python解释器**

Python和C/C++最大的区别：

C语言：

```
源代码
 ↓
编译器
 ↓
可执行文件
 ↓
运行
```

Python：

```
源代码(.py)
 ↓
Python解释器
 ↓
运行
```

例如，创建一个名为hello.py的文件，内容：

```python
print("Hello Python")
```

运行：

```bash
python3 hello.py
```

流程是：

```
hello.py
    |
    ↓
python3 interpreter
    |
    ↓
输出结果
```

**查看Python版本**

Linux中：

```bash
python3 --version
```

或者：

```bash
python3 -V
```

可能得到：

```text
Python 3.12.3
```

历史上存在Python 2和Python 3，Python 2 已经停止维护，现在默认学习 Python 3

**Python交互模式（REPL，Read-Eval-Print Loop）**

除了运行文件，还可以直接进入 Python

输入：

```bash
python3
```

会看到：

```text
Python 3.x.x

>>>
```

这个 >>> 叫作Python Prompt，现在可以直接输入代码，例如：

```python
>>> 1 + 2
3
>>> print("hello")
hello
```

退出：

```python
exit()
```

或者Linux也可以按Ctrl + D

**Python脚本文件**

实际开发中不会一直使用交互模式，而是创建脚本文件

创建：

```bash
touch hello.py
```

编辑：

```python
print("hello python")
```

运行：

```bash
python3 hello.py
```

输出：

```
hello python
```

**Python程序入口**

Linux中经常看到：

```python
#!/usr/bin/env python3

print("hello")
```

第一行：

```python
#!/usr/bin/env python3
```

它叫作shebang，负责告诉系统这个文件应该使用哪个解释器运行，例如：

先给运行权限：

```bash
chmod +x hello.py
```

然后直接运行：

```bash
./hello.py
```

另外，#！本身不是 Python 语法，它是 Unix/Linux 的脚本机制

**pip：Python包管理器**

**venv：Python虚拟环境工具**

这两部分在Linux笔记02-package-management.md中

**requirements.txt**

真实项目通常会记录依赖，例如：

```
requirements.txt
```

里面的内容：

```
numpy
pandas
torch
matplotlib
```

别人拿到项目，执行：

```bash
pip install -r requirements.txt
```

即可安装全部环境

**AI项目中的环境管理**

以后的项目大概这样：

```
mnist-project/

├── train.py
├── model.py
├── dataset.py
├── requirements.txt
└── .venv/
```

流程：

```bash
python3 -m venv .venv

source .venv/bin/activate

pip install 包名

python3 文件名
```
