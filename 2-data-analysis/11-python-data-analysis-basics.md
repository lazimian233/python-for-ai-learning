# Python数据分析基础（Python Data Analysis Basics）



**Python数据分析生态**

Python 在数据分析领域非常流行，主要依靠丰富的第三方库。常见生态：

```text
Python

├── NumPy
│   └── 数值计算

├── Pandas
│   └── 数据处理

├── Matplotlib
│   └── 数据可视化

├── Seaborn
│   └── 统计可视化

└── Scikit-learn
    └── 机器学习
```

这些库构成了 Python 数据分析的基础

- NumPy：主要用于数值计算、多维数组、矩阵运算、科学计算。是后续很多库的底层基础
- Pandas：主要用于读取数据、表格处理、数据清洗、数据统计。是 Python 数据分析中最重要的库之一
- Matplotlib：是 Python 最基础的可视化库，可以绘制折线图、柱状图、散点图、饼图等
- Seaborn：是建立在 Matplotlib 之上的高级可视化库，特点：代码更简单、默认效果更适合统计分析、适合探索数据关系

**Jupyter Notebook**

Jupyter Notebook 是数据分析中非常常用的交互式开发环境

传统 Python：

```text
写代码
 ↓
运行整个程序
 ↓
查看结果
```

Jupyter：

```text
写一小段代码
 ↓
立即运行
 ↓
查看结果
 ↓
继续下一步
```

代码可以分块运行，可以混合代码和文字，因此 Notebook 很适合数据分析报告、实验记录、Kaggle项目等

**安装数据分析库**

进入项目目录，先激活虚拟环境，然后执行：

```bash
pip install numpy pandas matplotlib seaborn jupyter
```

安装完成后在项目目录里生成requirements.txt：

~~~bash
pip freeze > requirements.txt
~~~

查看requirements.txt：

~~~bash
cat requirements.txt
~~~

**启动jupyter**

进入项目目录，先激活虚拟环境，然后执行：

~~~bash
jupyter notebook
~~~

输出的内容里会有网址，访问即可。打开后就会看到项目目录

另外也可以在vscode里编辑（要安装相应的拓展）：在项目目录里创建 .ipynb 文件，然后code 文件名即可用vscode打开它；另外要选择正确的python环境（虚拟环境）

**Python库导入规范**

数据分析中通常使用固定别名

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

**数据分析代码规范**

数据分析代码通常不是一次性运行，而是需要重复实验、修改参数、分享给别人，所以需要保持规范

- 导入放在开头

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
```

-  变量命名清晰

```python
user_data = pd.read_csv("users.csv")
```

- 保留分析步骤

```python
# 读取数据

# 查看数据结构

# 清洗数据

# 分析数据

# 可视化
```

- 使用 Notebook 记录过程


```text
提出问题
↓
尝试分析
↓
发现规律
↓
修改方案
```

**数据分析项目结构**

```text
data-analysis-project

├── data
│   └── dataset.csv
│
├── notebooks
│   └── analysis.ipynb
│
├── scripts
│   └── clean.py
│
├── README.md
│
└── requirements.txt
```

- data：存放数据（通常不提交过大的原始数据集）

- notebooks：存放分析过程
- scripts：存放正式 Python 文件
- requirements.txt：记录依赖