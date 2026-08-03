# 探索性数据分析（Exploratory Data Analysis, EDA）



现在把前面的知识结合起来，学习数据分析中非常重要的一步：探索性数据分析（EDA）

EDA 是数据分析项目中最常见的工作流程，也是 Kaggle 项目的核心步骤之一

它指的是：在正式建模或深入分析之前，通过统计方法和可视化手段探索数据，了解数据的结构、规律和潜在问题

简单来说就是：先认识数据，再分析数据

例如拿到一个新的数据集：

```text
students.csv
```

我们不知道：

- 有多少行？
- 有哪些字段？
- 有没有缺失值？
- 数据分布怎么样？
- 哪些变量相关？
- 有没有异常值？

EDA就是回答这些问题

**EDA的一个典型流程**：

```text
读取数据
    ↓
查看数据基本信息
    ↓
数据质量检查
    ↓
描述统计分析
    ↓
单变量分析
    ↓
变量关系分析
    ↓
可视化探索
    ↓
发现规律
```

## 读取数据

```python
import pandas as pd


df = pd.read_csv(
    "data.csv"
)
```

读取后第一步不是马上分析，而是：先了解数据

## 查看数据基本信息

```python
df.head()  查看前几行，了解数据格式、列名、样例数据
df.shape  查看数据形状
df.columns  查看列名
df.dtypes 检查数据类型
```

查看完整信息（行数，列数，列名，数据类型，非空数量）：

~~~
df.info()
~~~

## 数据质量检查

在分析之前，需要检查数据质量

主要包括：

```text
缺失值
重复值
错误数据
异常值
数据类型
```

- 缺失值检查

```python
df.isnull().sum()   查看每列的缺失值数量
```

```python
df.isnull().mean()  查看每列的缺失值所占比例（求布尔值的平均）
```

例如：

```text
age    0.1
```

表示：10%的数据缺失

- 重复值检查

数量：

```python
df.duplicated().sum()
```

删除：

```python
df.drop_duplicates()
```

## 描述统计分析

描述统计：使用统计指标快速了解数据特征

最常用：（默认只统计数值类型的列）

```python
df.describe()
```

输出：

| 指标  | 含义           |
| ----- | -------------- |
| count | 数量           |
| mean  | 平均值         |
| std   | 标准差         |
| min   | 最小值         |
| 25%   | 四分之一分位数 |
| 50%   | 中位数         |
| 75%   | 四分之三分位数 |
| max   | 最大值         |

可以快速了解平均水平、数据范围、波动程度等

如果想分析分类数据：

```python
df.describe(include="object")
```

输出：

| 指标   | 英文含义               | 含义               | 例子（gender列）    |
| ------ | ---------------------- | ------------------ | ------------------- |
| count  | 数量                   | 非空数据数量       | 5个性别数据         |
| unique | 唯一值数量             | 不同类别的数量     | Male、Female，共2种 |
| top    | top value（最高频值）  | 出现次数最多的类别 | Male                |
| freq   | frequency（频率/次数） | 最高频类别出现次数 | Male出现3次         |

## 单变量分析

单变量分析：分析一个变量自身的特点

**数值变量**

- 直方图：观察分布

```python
sns.histplot(
    data=df,
    x="score"
)
```

- 箱线图：观察异常值

```python
sns.boxplot(
    data=df,
    y="score"
)
```

**分类变量**

统计每个类别出现多少次：

```python
df["gender"].value_counts()
```

可视化：

```python
sns.countplot(
    data=df,
    x="gender"
)
```

【注】bar plot是通用的柱状图；count plot是专门用来统计分类变量的柱状图，先自动统计出每个类别出现多少次，再画图

## 变量关系分析

### 双变量分析

双变量分析：分析两个变量之间的关系

**数值 + 数值**

使用散点图观察趋势和相关关系，例如学习时间和成绩：

```python
sns.scatterplot(
    data=df,
    x="hours",
    y="score"
)
```

**数值 + 分类**

使用箱线图，例如班级和成绩：

```python
sns.boxplot(
    data=df,
    x="class",
    y="score"
)
```

**分类 + 分类**

使用交叉表，例如性别和是否通过：

```python
pd.crosstab(
    df["gender"],
    df["passed"]
)
```

### 分组统计

```python
df.groupby("分组列")["统计列"].统计方法()
```

返回的是Series/DataFrame

例如，统计不同班级平均成绩：

```python
df.groupby("class")["score"].mean()
```

结果：

```
A    85
B    90
C    88
```

可视化：(Seaborn 会默认计算平均值，这里是class → score平均值)

```python
sns.barplot(
    data=df,
    x="class",
    y="score"
)
```

### 相关性分析

相关性：衡量两个数值变量之间线性关系的强弱。不代表因果关系

相关系数的范围是 -1 ~ 1

| 范围 | 含义       |
| ---- | ---------- |
| 1    | 完全正相关 |
| 0    | 无线性相关 |
| -1   | 完全负相关 |

例如，分析 age和score之间的关系：

```python
df.corr()
```

结果：

```text
        age score

age     1    0.8

score 0.8    1
```

表示：age 和 score 具有较强正相关

用热力图可视化：

```python
sns.heatmap(
    df.corr(),
    annot=True   在热力图中显示具体数字
)
```

## EDA中的常见可视化组合

- 看数据分布

```text
describe()  描述统计
+
histplot()  直方图
+
boxplot()  箱线图
```

- 看变量关系

```text
scatterplot()   散点图
+
heatmap()   热力图
```

- 看类别数量

~~~
countplot()  分类变量数量统计图
~~~

- 看类别之间数值差异

~~~
barplot()  分类柱状图
~~~

- 看类别之间数值分布

```text
boxplot()  箱线图
```