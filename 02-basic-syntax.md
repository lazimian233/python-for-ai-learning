# 基本语法（Basic Syntax）



## 使用冒号和缩进表示代码块

例如，C语言：

```c
if (score >= 60) {
    printf("pass");
}
```

Python：

```python
if score >= 60:
    print("pass")
```

Python没有 { }，而是通过冒号和缩进表示代码块

通常是4个空格缩进

## 注释（Comment）

- 单行注释使用 #，例如：

```python
# this is a comment
```

解释器会直接忽略这一行

- 多行注释，Python没有真正的多行注释语法，通常使用多行字符串，例如：

```python
"""
这是多行文本
可以作为注释使用
"""
```

这里的三引号表示多行字符串，因为Python允许单独存在一个字符串，解释器会创建一个字符串对象，发现没用就丢弃了

它常用于给函数、类、模块写说明文档，叫作docstring（文档字符串）

也可以连续使用多个单行注释

## 变量（Variable）

变量用于保存数据。Python变量特点：

- 不需要声明类型，会自动判断类型

C语言：

```c
int age = 20;
```

Python：

```python
age = 20
```

- 变量类型可以改变

```python
x = 10         x是int类型

x = "hello"    x是str类型
```

这是Python的Dynamic Typing（动态类型）

变量命名规则：由字母、数字、下划线组成，不能以数字开头，不能包含特殊符号，不能使用关键字

## 关键字（Keywords）

| 常见的关键字 | 作用     |
| ------------ | -------- |
| if           | 条件     |
| else         | 否则     |
| for          | 循环     |
| while        | 循环     |
| class        | 定义类   |
| def          | 定义函数 |
| import       | 导入模块 |
| return       | 返回     |

## 数据类型（Data Types）

Python常见基础数据类型：

- int：integer，整数
- float：floating-point number，浮点数
- str：string，字符串，可以用单引号也可以用双引号括起来
- bool：boolean，布尔值，取值只有True和False，注意首字母必须大写
- NoneType：取值固定为None，表示没有值，注意首字母必须大写

int、float、str、bool 等类型名同时也是类；None 对象属于 NoneType 类型

**查看变量类型**使用 type( )，例如：

```python
x = 100

print(type(x))
```

输出：

```text
<class 'int'>
```

**类型转换（Type Conversion）**：不同类型之间可以转换

- 转整数

```python
x = int("100")
```

结果： x = 100

- 转浮点数

```python
x = float("3.14")
```

结果： x = 3.14

- 转字符串

```python
x = str(100)
```

结果： x = "100"

- 转布尔

```python
x = bool(1)
```

结果： x = True

注意：这些转换必须合理，像 int("hello") 这样的会报错

## 输入和输出

- 输出 print()，例如：

```python
print("Hello Python")
```

如果要输出多个值：

```python
name = "Tom"

print("Hello", name)
```

```text
Hello Tom
```

如果是表达式，会先计算出结果再输出

print()会自动在一次输出的多个值之间添加空格，可以手动修改sep参数，例如：

~~~python
print("Python", "Java", "C++", sep=",")
~~~

print()会自动在一次输出结束后添加换行符，可以手动修改end参数，例如：

~~~python
print(i, end=" ")     每次输出结束后添加空格，而不是换行
~~~

**格式化输出：f-string**，例如：

```python
epoch = 10
loss = 0.25

print(f"epoch={epoch}, loss={loss}")
```

输出：

```text
epoch=10, loss=0.25
```

会严格按照双引号（或单引号）中的形式来进行输出，其中：普通文字会原样输出；花括号中的内容会被当成表达式计算出结果，然后替换成结果再输出；遇到像\n这样的转义字符会进行转义

- 输入 input()，例如：

```python
name = input("请输入名字:\n")

print(name)
```

运行：

```text
请输入名字:
Tom
```

输出：

```text
Tom
```

input括号中的双引号中的内容会先输出，然后再等待用户输入

input得到的默认是字符串，如果需要的是数字，则需要进行类型转换，例如：

```python
age = int(input())
```