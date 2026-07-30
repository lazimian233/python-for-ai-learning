# Pandas基础（Pandas Basics）



## Pandas简介

Python Data Analysis Library，Python 中最重要的数据分析库之一

NumPy 解决的是：如何高效处理数值数组

但是现实中的数据通常不是简单的数字矩阵，而是带有行标签、列名称、不同数据类型的表格数据，例如：

| 姓名 | 年龄 | 城市 | 成绩 |
| ---- | ---- | ---- | ---- |
| Tom  | 18   | 北京 | 90   |
| Jack | 19   | 上海 | 85   |
| Lucy | 18   | 广州 | 95   |

这种数据就是 Pandas 的主要应用场景

## Series和DataFrame：Pandas核心数据结构

可以理解为：

```text
Series
 ↓
一维带标签数组


DataFrame
 ↓
二维带标签表格
```

## Series（一维数据）

带标签的一维数组，类似于：

```text
NumPy ndarray
+
索引(index)
```

默认格式：（其中索引可以自定义）

```text
索引(index)    数据(value)

0              90
1              80
2              70
```

**创建 Series**

```python
import pandas as pd

s = pd.Series([90,80,70])

print(s)
```

输出：

```text
0    90
1    80
2    70
dtype: int64
```

通过索引访问：

~~~python
s[0]
~~~

结果：

~~~
90
~~~

**自定义索引**

```python
s = pd.Series(
    [90,80,70],
    index=["Tom","Jack","Lucy"]
)

print(s)
```

输出：

```text
Tom     90
Jack    80
Lucy    70
```

通过标签索引访问：

```python
s["Tom"]
```

结果：

```text
90
```

通过位置索引访问：

~~~python
s.iloc[0]
~~~

结果：

~~~
90
~~~

## DataFrame（二维表格）

DataFrame 是 Pandas 最核心的数据结构

可以理解为：多个 Series 共享同一个索引组成的二维带标签数据结构，例如：

```python
data = {
    "name":["Tom","Jack","Lucy"],
    "age":[18,19,18],
    "score":[90,85,95]
}

df = pd.DataFrame(data)
```

输出：

```text
    name   age   score
0    Tom    18      90
1   Jack    19      85
2   Lucy    18      95
```

结构：

```text
              columns

          name   age   score

index 0    Tom    18      90
index 1   Jack    19      85
index 2   Lucy    18      95
```

**DataFrame和NumPy数组的区别**

- NumPy数组：

```python
arr = np.array([
    [18,90],
    [19,85]
])
```

```text
18 90
19 85
```

不知道这些数据代表什么

- DataFrame：

```text
        age score

Tom      18   90
Jack     19   85
```

拥有行标签(index)、列标签(columns)、数据类型(dtype)，因此更适合处理现实数据

另外，这里的索引不是默认的0、1，而是Tom、Jack，也是**自定义索引**：

~~~python
df = pd.DataFrame(
    {
        "age":[18,19],
        "score":[90,85]
    },
    index=["Tom","Jack"]
)
~~~

## 创建DataFrame

**使用字典（最常用）**

```python
df = pd.DataFrame({
    "name":["Tom","Jack"],
    "age":[18,19]
})
```

字典的key变成列标签，字典的value列表变成列数据，结果：

~~~
    name   age
0    Tom    18
1   Jack    19
~~~

**使用列表**

```python
data = [
    ["Tom",18],
    ["Jack",19]
]

df = pd.DataFrame(
    data,
    columns=["name","age"]
)
```

二维列表中的每个子列表代表一行数据，指定列标签，结果：

```text
    name age

0    Tom 18
1   Jack 19
```

## 查看DataFrame信息

创建：

```python
df = pd.DataFrame({
    "name":["Tom","Jack","Lucy"],
    "age":[18,19,18],
    "score":[90,85,95]
})
```

结果：

~~~
    name   age   score
0    Tom    18      90
1   Jack    19      85
2   Lucy    18      95
~~~

**df.head()：查看前几行**

默认查看前5行，也可以指定查看的行数：

```python
df.head(2)    查看前2行
```

结果：
~~~
    name   age   score
0    Tom    18      90
1   Jack    19      85
~~~

**df.tail()：查看后几行**

默认查看后5行，也可以指定查看的行数：

~~~
df.tail(2)    查看后2行
~~~

结果：

~~~
    name   age   score
1   Jack    19      85
2   Lucy    18      95
~~~

**df.shape：查看形状**

规则和NumPy一样

结果：

```text
(3,3)       表示3行3列
```

**df.columns：查看列标签**

结果：

```text
Index(['name','age','score'])
```

**df.dtypes：查看数据类型**

结果：

```text
name     object
age       int64
score     int64
```

**df.info()：查看完整信息**

显示行数、列数、列名、数据类型、非空数量

结果：（这里的具体输出格式会随着 Pandas版本略有变化）

~~~
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 3 entries, 0 to 2
Data columns (total 3 columns):
Column  Non-Null Count  Dtype
name    3 non-null      object
age     3 non-null      int64
score   3 non-null      int64
~~~

## DataFrame选择数据

**选择一列**

```python
df["score"]
```

结果：（变成了Series）

```text
0    90
1    85
2    95
```

**选择多列**

```python
df[["name","score"]]
```

注意：这里有两个中括号，外层表示选择数据，内层表示列名列表

结果：（仍然是DataFrame）

```text
    name score

0    Tom    90
1   Jack    85
2   Lucy    95
```

**loc：按标签选择**

location，根据标签选择，例如：

```python
df.loc[0]
```

选择第0行，结果：（返回Series）

~~~
name     Tom
age       18
score     90
~~~

```python
df.loc[0,"score"]
```

选择第0行的score列，结果：

~~~
90
~~~

**iloc：按位置选择**

integer location，根据数字位置选择，例如：

```python
df.iloc[0]
```

选择第0行，结果：（返回Series）

~~~
name     Tom
age       18
score     90
~~~

~~~python
df.iloc[0,2]
~~~

选择第0行第2列，结果：

```text
90
```

【注1】索引（行标签）和列标签不属于数据本身，不计入列数和行数

【注2】如果选择的是某一行或某一列的话，通常会降维，返回的是Series；如果选择的是某个具体位置的话，只返回这一个位置的元素；如果选择的是一个多行多列的范围的话，返回的仍然是DataFrame

【注3】使用单个列标签选择单列时返回 Series；使用列表选择列时保持 DataFrame，比如这样：

~~~python
df[["score"]]
或者
df.loc[:,["score"]]
~~~

【注4】loc和iloc依旧是以逗号作为分隔符，前面指定行，后面指定列；只指定行时可以省略逗号和后面的列

| 方式 | 依据 |
| ---- | ---- |
| loc  | 标签 |
| iloc | 位置 |

**数据筛选**

- 只有一个条件

例如，筛选成绩大于90的数据：

```python
df[df["score"] > 90]
```

首先，df["score"] > 90，得到：

```text
False
False
True
```

这叫作：布尔索引（Boolean Indexing），然后再筛选出结果为True的数据，结果：

~~~
    name age score
2   Lucy  18   95
~~~

- 多个条件

例如，筛选年龄18并且成绩大于90的数据：

```python
df[
    (df["age"] == 18)
    &
    (df["score"] > 90)
]
```

注意：Pandas中，& 表示与，| 表示或，~ 表示非，不能使用 and、or、not

## 添加和修改列

**添加新列**

例如：

```python
df["passed"] = df["score"] >= 60

df["新列名"] = 新列的内容
```

结果：

```text
    name age score passed
0    Tom  18   90   True
1   Jack  19   85   True
2   Lucy  18   95   True
```

**修改列**

例如：

```python
df["score"] = df["score"] + 5
```

所有成绩增加5，结果：

~~~
    name age score
0    Tom  18   95
1   Jack  19   90
2   Lucy  18   100
~~~

## 常用统计函数

Pandas很多统计函数和 NumPy 类似

- 平均值：

```python
df["score"].mean()
```

- 最大值：

```python
df["score"].max()
```

- 最小值：

```python
df["score"].min()
```

- 统计描述：

```python
df.describe()
```

输出：数量、平均值、标准差、最大值、最小值、四分位数

这些函数返回计算结果，不会修改原 DataFrame