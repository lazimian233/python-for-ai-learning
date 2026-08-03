# 数据处理（Data Processing）



实际项目中的数据通常不是直接可以分析的，可能存在缺失值、重复数据、异常值、格式不统一等问题

因此需要先进行数据处理，将原始数据转换成适合分析的数据

Pandas中的大部分数据处理方法默认不会修改原DataFrame，而是返回新的DataFrame或Series，如果想保存，需要像这样：

~~~python
df = df.dropna()
~~~

一个典型的数据分析流程：

```text
原始数据
    ↓
数据读取
    ↓
数据初步检查
    ↓
数据清洗
    ↓
数据转换
    ↓
数据整理
    ↓
数据分析
```

## 数据读取

实际项目中，数据通常来自CSV文件/Excel文件/数据库/API接口等，其中最常见的是csv文件

**读取CSV文件**

例如：students.csv

```csv
name,age,score
Tom,18,90
Jack,19,85
Lucy,18,95
```

读取：

```python
import pandas as pd

df = pd.read_csv("students.csv")
```

读取后：

```text
    name   age   score

0   Tom    18     90
1   Jack   19     85
2   Lucy   18     95
```

读取 CSV 文件时，Pandas 会根据数据内容自动推断数据类型；对于无法自动判断或需要特殊处理的数据，需要手动进行类型转换

所以读取完文件后记得进行类型检查

**读取Excel文件**

需要先安装：

```bash
pip install openpyxl
```

读取：

```python
df = pd.read_excel("students.xlsx")
```

---

## 数据初步检查

拿到数据后，先初步了解数据

**查看前几行**

```python
df.head()
```

**查看后几行**

```python
df.tail()
```

**查看数据规模**

```python
df.shape
```

**查看列名**

```python
df.columns
```

**查看数据类型**

```python
df.dtypes
```

**查看完整信息**

```python
df.info()
```

可以查看：行数、列数、列名、数据类型、非空数量

---

## 数据清洗

### 缺失值处理

缺失值就是数据中不存在的值，Pandas通常使用 NaN 来表示，例如：

| name | age  | score |
| ---- | ---- | ----- |
| Tom  | 18   | 90    |
| Jack | NaN  | 85    |
| Lucy | 18   | 95    |

**查看缺失值**

```python
df.isnull()
```

结果：（返回布尔值，True表示数据缺失）

```text
name    age    score

False  False   False
False   True   False
False  False   False
```

**统计缺失值数量**

```python
df.isnull().sum()
```

结果：

```text
name     0
age      1
score    0
```

表示：age列有一个缺失值

**删除缺失值**

删除包含缺失值的行：

```python
df.dropna()
```

例如，原数据：

```text
Tom     18    90
Jack    NaN   85
Lucy    18    95
```

结果：

```text
Tom     18    90
Lucy    18    95
```

**填充缺失值**

- 使用固定值填充，例如使用0填充：

```python
df.fillna(0)
```

- 使用统计值填充，例如使用平均值填充：

```python
df["age"].fillna(
    df["age"].mean()
)
```

原数据：

```text
18
NaN
20
```

平均为19，所以填充后：

```text
18
19
20
```

### 重复数据处理

可能有的数据会重复出现多次

**查看重复数据**

```python
df.duplicated()
```

结果：

```text
False
False
True
```

表示：第三行数据与之前的数据重复

**删除重复数据**

```python
df.drop_duplicates()
```

例如，原数据：

```text
Tom    18    90
Jack   19    85
Tom    18    90
```

结果：

```text
Tom    18    90
Jack   19    85
```

### 错误数据处理

数据本身有问题，比如无法解析、格式错误、逻辑错误等

例如，现在age这一列是object类型，要转换成int

~~~
"18"
"20"
"abc"
~~~

其中，“abc”无法解析成数字，属于错误数据，处理：

~~~python
df["age"] = pd.to_numeric(
    df["age"],
    errors="coerce"
)
~~~

其中errors="coerce”表示：无法转换的数据变成 NaN

结果：

~~~
18
20
NaN
~~~

然后再结合df.dropna( )进行处理

它和普通的数据类型转换的区别：

- astype() ：已知数据都合法，只改变类型；一旦里面有无法转换的错误数据，会直接报错
- pd.to_numeric() ：尝试把数据转换成数字，并处理无法转换的数据，更适合处理脏数据

### 异常数据处理

异常值是明显偏离正常范围的数据，有可能是真的，也有可能是假的，需要根据业务规则或统计方法判断。例如：

```
成绩：

90
85
95
10  远离其他数据，是异常值，但也有可能真的是10分，所以不能直接删除，需要具体判断
```

具体异常值检测方法将在探索性数据分析章节学习

---

## 数据转换

### 数据类型转换

数据读取后，有时类型不正确，例如：

```text
age

18
19
20
```

实际它们的类型可能是 object 而不是 int64

**查看数据类型**

```python
df.dtypes
```

**转换数据类型**

比如把age这一列的数据类型转换为int

```python
df["age"] = df["age"].astype(int)
```

### 数据格式转换

**日期格式转换（最常见）**

例如，以下原始数据都是日期，但格式不统一：

```
2026/08/03
08-03-2026
2026年8月3日
```

转换：

```python
df["date"] = pd.to_datetime(df["date"])
```

统一成 Pandas 的日期类型：

```
2026-08-03
```

**字符串格式转换**

例如，以下用户姓名的字符串存在前后空格、大小写不统一的问题：

```
" tom "
"JACK"
"Lucy"
```

去除空格：

```
df["name"] = df["name"].str.strip()
```

统一大小写：

```
df["name"] = df["name"].str.lower()
```

结果：

```
tom
jack
lucy
```

**单位格式转换**

例如，原始的身高数据带单位，但是分析时希望使用纯数字：

```
170cm
175cm
180cm
```

转换：

```python
df["height"] = (
    df["height"]
    .str.replace("cm","")
    .astype(int)
)
```

结果：

~~~
170
175
180
~~~

单位换算：对包含单位的数据，需要先提取数值和单位，再按照规则进行换算

### 数据结构调整

- 宽表：同一个实体的信息分布在多个列中，表横向展开

行表示实体，列表示属性

| name | math | english | physics |
| ---- | ---- | ------- | ------- |
| Tom  | 90   | 85      | 88      |
| Jack | 80   | 95      | 90      |

- 长表：把原来的多个列变成一列分类信息，表纵向增长

一列表示变量，一列表示变量值

| name | subject | score |
| ---- | ------- | ----- |
| Tom  | math    | 90    |
| Tom  | english | 85    |
| Tom  | physics | 88    |
| Jack | math    | 80    |
| Jack | english | 95    |
| Jack | physics | 90    |

不同场景需要不同的结构格式：宽表适合人阅读，长表适合数据分析

**宽表 → 长表**

```
pd.melt()     把多个列压缩成一列
```

例如现在有宽表：

```
    name  math  english  physics

0   Tom    90      85       88
1  Jack    80      95       90
```

转换：

```python
long_df = pd.melt(
    wide_df,
    id_vars=["name"],      这一列不参与转换，保留
    value_vars=["math","english","physics"],     这些列需要被转换
    var_name="subject",        新生成的分类列标签，这一列放原来的列标签
    value_name="score"         原来列里的值放在这一列
)
```

结果：

| name | subject | score |
| ---- | ------- | ----- |
| Tom  | math    | 90    |
| Jack | math    | 80    |
| Tom  | english | 85    |
| Jack | english | 95    |
| Tom  | physics | 88    |
| Jack | physics | 90    |

**长表 → 宽表**

```
pivot()     把某一列分类重新展开成多个列
```

例如现在有长表：

| name | subject | score |
| ---- | ------- | ----- |
| Tom  | math    | 90    |
| Tom  | english | 85    |
| Jack | math    | 80    |

转换：

```python
wide_df = long_df.pivot(
    index="name",          原来的这一列变成行索引
    columns="subject",     原来的这一列变成列标签
    values="score"         原来的这一列变成填充的数据
)
```

结果：

|      | math | english |
| ---- | ---- | ------- |
| Tom  | 90   | 85      |
| Jack | 80   |         |

如果需要把行索引恢复为普通列，可以：

```python
wide_df.reset_index()
```

## 数据整理

### 排序

按照某列排序，默认**升序**：

```python
df.sort_values("score")
```

结果：

```text
Jack    85
Tom     90
Lucy    95
```

如果要**降序**：

```python
df.sort_values(
    "score",
    ascending=False
)
```

结果：

```text
Lucy    95
Tom     90
Jack    85
```

### 筛选

**只有一个条件**

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

**多个条件**

例如，筛选年龄18并且成绩大于90的数据：

```python
df[
    (df["age"] == 18)
    &
    (df["score"] > 90)
]
```

注意：Pandas中，& 表示与，| 表示或，~ 表示非，不能使用 and、or、not

### 修改

- 修改列名，比如把score改成grade：

```python
df.rename(
    columns={
        "score":"grade"
    }
)
```

- 删除列，比如删除age这一列：

```python
df.drop(
    columns=["age"]
)
```

- 数据替换，比如把city中的北京替换为Beijing：

```python
df["city"] = df["city"].replace(
    "北京",
    "Beijing"
)
```

### 合并

实际项目中，数据通常来自多个表，需要把它们合并到一起

**pd.merge()：根据共同字段合并**

默认只保留两个DataFrame中id都存在的数据（inner join）

例如，要合并学生信息df1 和成绩信息df2：

| id   | name |
| ---- | ---- |
| 1    | Tom  |
| 2    | Jack |

| id   | score |
| ---- | ----- |
| 1    | 90    |
| 2    | 85    |

```python
pd.merge(
    df1,
    df2,
    on="id"
)
```

结果：

| id   | name | score |
| ---- | ---- | ----- |
| 1    | Tom  | 90    |
| 2    | Jack | 85    |

**pd.concat()：直接拼接多个 DataFrame**

例如，要直接拼接两个表：

```
df1:

Tom
Jack


df2:

Lucy
Bob
```

合并：

```python
pd.concat(
    [df1,df2]
    axis=0    纵向拼接（如果等于1的话就是横向拼接）
)
```

结果：

```
Tom
Jack
Lucy
Bob
```

### 保存

以上处理完成后，保存CSV文件：

```python
df.to_csv(
    "clean_data.csv",
    index=False
)
```

其中 index=False 表示：不保存DataFrame的索引

否则就会多出一列：

```text
,index,name,age
0,Tom,18
1,Jack,19
```