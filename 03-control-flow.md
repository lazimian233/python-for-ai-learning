# 流程控制（Control Flow）



## 条件判断（Conditional Statements）

根据不同情况执行不同代码，基本格式：

```python
if 条件1:
    代码块1
elif 条件2:
	代码块2
else:
	代码块3
```

可以只有 if；可以有 if + elif；可以有 if + elif + else

一个例子：

```python
score = 85

if score >= 90:
    print("A")
elif score >= 80:
    print("B")
elif score >= 60:
    print("C")
else:
    print("D")
```

**条件表达式**

if后面的条件最终必须得到True或False的结果

另外，python认为非0数字相当于True，0相当于False，这种转换规则通过 bool() 函数实现。所以：

```python
x = 10

if x:
    print("yes")
```

会执行

常见的真假判断：

| 值         | bool结果 |
| ---------- | -------- |
| 非0数字    | True     |
| 0          | False    |
| 非空字符串 | True     |
| 空字符串"" | False    |
| 空列表[]   | False    |
| 空字典{}   | False    |
| 空元组()   | False    |
| None       | False    |

| 比较运算符 | 含义     |
| ---------- | -------- |
| >          | 大于     |
| <          | 小于     |
| >=         | 大于等于 |
| <=         | 小于等于 |
| ==         | 等于     |
| !=         | 不等于   |

| 逻辑运算符 | 含义         |
| ---------- | ------------ |
| and        | 同时满足     |
| or         | 满足一个即可 |
| not        | 取反         |

## 循环（Loops）

重复执行代码，主要有for循环和while循环

- for循环的基本结构：

```python
for 变量 in 序列:
    执行代码
```

例如：

```python
for i in range(5):
    print(i)
```

输出：

```text
0
1
2
3
4
```

**range( )用于生成数字序列**

- 一个参数

~~~python
range(end)
~~~

例如 range(5) 生成：

```text
0 1 2 3 4       （从0开始，不包含参数本身）
```

- 两个参数

```python
range(start, end)
```

例如 range(2,6) 生成：

```text
2 3 4 5          （从第一个参数开始，不包含第二个参数）
```

- 三个参数

```python
range(start, end, step)
```

例如 range(0,10,2) 生成：

```text
0 2 4 6 8         （第三个参数表示每次增加多少）
```

- while循环的基本结构：

```python
while 条件:
    执行代码
```

当满足条件时会持续执行

必须保证条件最终变为False，否则会陷入无限循环

## 循环控制

- break：立即结束当前循环

例如：

```python
for i in range(10):
    if i == 5:
        break

    print(i)
```

输出：

```text
0
1
2
3
4
```

当i == 5时退出循环

- continue：跳过当前这一次循环，继续下一次

例如：

```python
for i in range(5):

    if i == 2:
        continue

    print(i)
```

输出：

```text
0
1
3
4
```

当i ==2时跳过当前这一次循环，不会print，直接进入下一次循环

- pass：什么也不做，占位

为什么需要pass呢？因为Python要求代码块必须包含至少一条语句

例如：

```python
if age > 18:
```

会报错。应改为：

```python
if age > 18:
    pass
```

## enumerate()：同时获得元素和索引

例如，普通方式：

```python
names = ["Tom","Bob","Alice"]

for i in range(len(names)):
    print(i,names[i])
```

比较麻烦。使用enumerate：

```python
names = ["Tom","Bob","Alice"]

for index,name in enumerate(names):
    print(index,name)
```

输出：

```text
0 Tom
1 Bob
2 Alice
```

## zip()：同时遍历多个序列

例如：

```python
names = ["Tom","Bob"]
scores = [90,80]

for name,score in zip(names,scores):
    print(name,score)
```

输出：

```text
Tom 90
Bob 80
```

zip会按照最短的序列长度进行匹配，多余元素会被忽略