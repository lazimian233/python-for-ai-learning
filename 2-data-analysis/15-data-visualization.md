# 数据可视化（Data Visualization）



数据分析不仅需要计算结果，还需要把结果展示出来，让人能够直观看到数据规律，这就是数据可视化

使用图形化方式展示数据，使数据中的规律、趋势和关系更加直观

**Python中常用的数据可视化库：**

Matplotlib：最基础、最重要的绘图库

```python
import matplotlib.pyplot as plt
```

Seaborn：基于 Matplotlib 的高级可视化库

```python
import seaborn as sns
```

## Matplotlib基础

### 折线图

plot()：绘制数据点，并默认使用线连接数据点，因此常用于绘制折线图，例如：

```python
import matplotlib.pyplot as plt


x = [1,2,3,4]
y = [10,20,15,30]


plt.plot(x,y)

plt.show()
```

一个图像通常包含：

```text
标题(title)

        y轴
        ↑
        |
数据区域
        |
        +------------→
              x轴

图例(legend)
```

**创建折线图**

```python
plt.plot()
```

**显示图像**

```python
plt.show()
```

**添加标题**

```python
plt.title("Sales Trend")
```

**添加x轴标签**

```python
plt.xlabel("Month")
```

**添加y轴标签**

```python
plt.ylabel("Sales")
```

**设置线条样式**

- 颜色

```python
plt.plot(
    x,
    y,
    color="red"
)
```

- 线宽

```python
plt.plot(
    x,
    y,
    linewidth=2
)
```

- 标记数据点

```python
plt.plot(
    x,
    y,
    marker="o"   每个数据点显示圆点
)
```

**绘制多个数据**

例如，比较两个产品销量：

```python
month = [1,2,3,4]

product_A = [10,20,30,40]

product_B = [20,25,35,45]


plt.plot(
    month,
    product_A,
    label="A"
)

plt.plot(
    month,
    product_B,
    label="B"
)
```

添加A线和B线的图例：

```python
plt.legend()
```

### 柱状图（Bar Chart）

用柱子的高度比较不同类别的数据

例如，城市人口：

```python
cities = ["Beijing","Shanghai","Guangzhou"]

population = [2000,2500,1500]
```

绘制：

```python
plt.bar(
    cities,
    population
)

plt.show()
```

### 散点图（Scatter Plot）

用点表示两个变量之间的关系，可以观察两个变量是否相关（相关性不代表因果）

例如，学习时间和成绩：

```python
hours = [1,2,3,4,5]

score = [60,65,75,85,95]
```

绘制：

```python
plt.scatter(
    hours,
    score
)
```

### 直方图（Histogram）

展示数据分布情况

例如，学生成绩：

```text
60
70
75
80
90
95
```

绘制：

```python
plt.hist(score)
```

| 图表                 | 横轴（x轴）     | 纵轴（y轴） | 关注的问题             |
| -------------------- | --------------- | ----------- | ---------------------- |
| **柱状图 Bar Chart** | 分类            | 数值        | 不同类别之间的大小差异 |
| **直方图 Histogram** | 数值区间（bin） | 频数/数量   | 数据集中在哪里         |

## Seaborn基础

Seaborn通常直接使用DataFrame，通过列名指定变量，不需要手动提取

### 散点图（Scatter Plot）

```python
sns.scatterplot(
    data=df,
    x="age",
    y="score"
)
```

### 分类柱状图（Bar Plot）

```python
sns.barplot(
    data=df,
    x="city",
    y="score"
)
```

### 箱线图（Box Plot）

用于观察数据分布、异常值

```python
sns.boxplot(
    data=df,
    y="score"
)
```

### 热力图（Heatmap）

常用于相关性分析，用颜色表示变量之间相关性的强弱

```python
sns.heatmap(
    df.corr()
)
```

## Pandas快速绘图

Pandas内部也封装了 Matplotlib

例如：

```python
df["score"].plot()
```

相当于：

```python
plt.plot(
    df["score"]
)
```

## Figure 和 Axes

```
Figure（整张画布）
┌─────────────────────────────┐
│                             │
│       Axes（绘图区）          │
│                             │
│          y                  │
│          ↑                  │
│          |                  │
│          |        *         │
│          |     *            │
│          |  *               │
│          └──────────→ x     │
│                             │
└─────────────────────────────┘
```

- Figure：整张图像的容器（画布）

例如：

```
fig
```

表示整张图，负责图像大小/保存图片/包含多个子图

- Axes：真正绘制数据的区域

前面见过的axis是一根轴，而Axes（注意首字母大写）表示一个坐标系区域，多个 Axes 对象组成 axes 数组

包含坐标轴/数据曲线/标题/标签

例如：

```
ax.plot(x,y)
```

是在这个 Axes 上画图

**pyplot方式 vs 面向对象方式**

现在学的是：

```python
import matplotlib.pyplot as plt

plt.plot(x,y)

plt.show()
```

这是pyplot接口，它背后帮你创建Figure和Axes，所以不用管

实际上：

```
plt.plot(x,y)
```

类似于：

```python
fig = plt.figure()   创建画布fig
  
ax = fig.add_subplot(111)  创建一个1行1列的布局，并选择第1个位置，在这个位置创建子图ax

ax.plot(x,y)       画图
```

更标准的写法：

```python
import matplotlib.pyplot as plt


x = [1,2,3,4]
y = [10,20,15,30]


fig, ax = plt.subplots()   创建Figure对象fig和Axes对象ax


ax.plot(x,y)


plt.show()
```

- 设置标题：

```
ax.set_title()
```

- 设置标签：

```
ax.set_xlabel()

ax.set_ylabel()
```

完整：

```
fig, ax = plt.subplots()


ax.plot(x,y)

ax.set_title("Sales Trend")

ax.set_xlabel("Month")

ax.set_ylabel("Sales")


plt.show()
```

**为什么要学这种写法**

简单情况下 plt.plot() 够用

但是如果有多个图，例如要比较两个模型：

```
Figure
┌────────────┐
│ Axes1      │
│            │
├────────────┤
│ Axes2      │
│            │
└────────────┘
```

代码：

```
fig, axes = plt.subplots(2,1)   创建一个 Figure，并在里面创建2行1列的两个 Axes（两个子图）
```

得到：

```
axes[0]  控制Axes1

axes[1]  控制Axes2
```

1行2列的情况：

~~~
Figure

┌──────────┬──────────┐
│          │          │
│ axes[0]  │ axes[1]  │
│          │          │
└──────────┴──────────┘
~~~

2行2列的情况：

~~~
Figure

┌─────────┬─────────┐
│axes[0,0]│axes[0,1]│
├─────────┼─────────┤
│axes[1,0]│axes[1,1]│
└─────────┴─────────┘
~~~

如果只用plt.plot()的话，管理多个图会很麻烦

## 保存图像

**Matplotlib保存**

```
plt.savefig()
```

例如：

```python
plt.plot(x,y)

plt.savefig(
    "result.png",
    dpi=300
)
```

**常用参数**：

| 参数                  | 作用         |
| --------------------- | ------------ |
| `dpi`                 | 图片清晰度   |
| `bbox_inches="tight"` | 去除多余空白 |
| `transparent=True`    | 透明背景     |
| `facecolor`           | 设置背景颜色 |

**保存格式**：Matplotlib支持png/jpg/pdf/svg

- png/jpg：位图，放大后像素变大，适合报告、网页等
- pdf/svg：矢量图，放大后仍然清晰，适合论文、出版等

**保存路径**：

- 如果只写：

```python
plt.savefig("result.png")
```

会保存到当前工作目录，例如：

```
project/

├── main.py
└── result.png
```

- 也可以指定路径：

```python
plt.savefig(
    "images/result.png"
)
```

保存到：

```
project/

├── images/
│   └── result.png
│
└── main.py
```

**Figure保存**

使用面向对象方式：

```python
fig, ax = plt.subplots()

ax.plot(x,y)

fig.savefig(
    "result.png"
)
```

**Seaborn保存**

Seaborn基于Matplotlib，因此仍然使用：

```
plt.savefig()
```

或者：

~~~
fig.savefig()
~~~

例如：

~~~python
import seaborn as sns
import matplotlib.pyplot as plt


sns.scatterplot(
    data=df,
    x="age",
    y="score"
)


plt.savefig(
    "scatter.png",
    dpi=300,
    bbox_inches="tight"
)

plt.show()
~~~

或者使用面向对象写法：

~~~python
import seaborn as sns
import matplotlib.pyplot as plt


fig, ax = plt.subplots()


sns.scatterplot(
    data=df,
    x="age",
    y="score",
    ax=ax
)


ax.set_title("Age vs Score")


fig.savefig(
    "scatter.png",
    dpi=300
)


plt.show()
~~~

其中的参数：

```
ax=ax
```

表示：使用已经创建好的 Axes，而不是自己创建新的。如果有多个子图就写成这样的：

~~~python
ax=axes[0]
~~~

【注1】先save再show，因为show完可能会关闭当前图像

【注2】做 Kaggle 项目时，最常用的是 `png + dpi=300 + bbox_inches="tight"`，比如把 EDA 图保存到项目报告中

【注3】如果一个程序里有fig1、fig2、fig3这样的多个图，推荐在面向对象写法中使用 `fig.savefig()` 保存指定 Figure，因为plt.savefig()容易保存错当前图