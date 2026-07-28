# 核心数据结构（Core Data Structures）



数据结构用于组织和存储数据，使程序能够高效地访问和处理数据

Python中常见的数据结构：

| 类型   | 英文       | 特点                                 |
| ------ | ---------- | ------------------------------------ |
| 字符串 | string     | 保存文本，**不可变**                 |
| 列表   | list       | 保存多个元素，有序，**可变**         |
| 元组   | tuple      | 保存多个元素，有序，**不可变**       |
| 字典   | dictionary | 保存键值对，**可变**                 |
| 集合   | set        | 保存多个元素，无序、不重复，**可变** |

是否可变，也就是创建后里面的元素还能否再修改

是否可变决定了：像.什么什么() 这样的方法是否会修改它自身

可变→方法通常可以修改原对象

不可变→方法通常不能修改原对象，而是返回新对象，要想保存修改结果的话需要重新赋值

## String（字符串）

保存文本，不可变，用双引号（或单引号）括起来，例如：

```python
word = "Python"
```

**字符串索引**：字符串中的每个字符都有位置，索引默认从0开始

```text
 P  y  t  h  o  n
 0  1  2  3  4  5
```

例如：

```python
print(word[0])
```

输出：

```text
P
```

负索引：Python也支持从后往前访问，此时最后一个字符的索引为-1，越往前越小

```text
 P  y  t  h  o  n
-6 -5 -4 -3 -2 -1
```

例如：

```python
print(word[-1])
```

输出：

```text
n
```

**字符串切片**：格式如下

```python
string[start:end]
```

包含start，不包含end

例如：

```python
word = "Python"

print(word[0:3])
```

输出：

```text
Pyt
```

省略参数的情况：

- 省略参数1，说明从开头开始

```python
word[:参数2]
```

- 省略参数2，说明到结尾结束

```python
word[参数1:]
```

- 两个参数都省略，说明全部复制

~~~python
word[:]
~~~

**字符串拼接**：使用 + 连接，例如：

```python
first = "Hello"
second = "Python"

print(first + second)
```

输出：

```text
HelloPython
```

如果需要空格：

```python
print(first + " " + second)
```

输出：

```text
Hello Python
```

**len()：获取字符串长度**

```python
word = "Python"

print(len(word))
```

输出：

```text
6
```

**.lower()：转换为小写**

```python
"HELLO".lower()
```

结果：

```text
hello
```

**.upper()：转换为大写**

```python
"hello".upper()
```

结果：

```text
HELLO
```

**.replace()：把其中一部分替换为其他内容**

```python
text = "I like Java"

text.replace("Java","Python")
```

结果：

```text
I like Python
```

**.split()：把字符串分割为字符串列表**

```python
text = "a,b,c"

text.split(",")
```

结果：

```python
['a','b','c']
```

## List（列表）

保存多个元素、有序、可变，例如：

```python
numbers = [1,2,3]
names = ["Tom","Bob","Alice"]
data = [1,"hello",True]
```

Python允许不同数据类型混合

**列表索引、列表切片**：同字符串

**修改元素：**

```python
names[0] = "Jack"
```

结果：

```python
["Jack","Bob","Alice"]
```

**.append()：在末尾添加元素**

```python
numbers = [1,2,3]

numbers.append(4)
```

结果：

```text
[1,2,3,4]
```

**.insert()：在指定索引位置添加元素，原位置的元素依次往后移**

```python
numbers.insert(1,10)
```

结果：

```text
[1,10,2,3]
```

**.extend()：把一个列表合并到另一个列表之后**

```python
a=[1,2]

b=[3,4]

a.extend(b)
```

结果：

```text
[1,2,3,4]
```

**.remove()：删除指定值**

```python
numbers = [1,2,3]

numbers.remove(2)
```

结果：

~~~python
[1,3]
~~~

**.pop()：删除指定索引位置的元素**

```python
numbers.pop(0)
```

结果：

~~~
[2,3]
~~~

如果不指定索引的话，numbers.pop()默认删除最后一个元素

**列表遍历**

- 普通方式：


```python
numbers=[1,2,3]

for x in numbers:
    print(x)
```

输出：

```text
1
2
3
```

- 带索引：


```python
for i,x in enumerate(numbers):
    print(i,x)
```

输出：

```text
0 1
1 2
2 3
```

**列表推导式（List Comprehension）**

Python常用写法

例如：生成一个元素为0~4的整数的列表

- 普通方式：


```python
numbers=[]

for i in range(5):
    numbers.append(i)
```

- 列表推导式：


```python
numbers=[i for i in range(5)]
```

结果：

```text
[0,1,2,3,4]
```

## Tuple（元组）

Tuple 和 List 很像，都是保存多个元素、有序，例如：

List：

```python
numbers = [1,2,3]
```

Tuple：

```python
numbers = (1,2,3)
```

最大的区别是：List 可变，Tuple 不可变

**创建Tuple**：使用( )，例如：

```python
point = (10,20)
```

也可以不写( )，python会自动认为这是一个元组(10,20)

```python
point = 10,20
```

**元组索引、元组切片**：同字符串和列表

string、list、tuple都属于python中的序列类型，它们的索引和切片规则基本完全一样，都支持正负索引，切片都不会改变原对象

**Tuple不可修改**

```python
point = (10,20)

point[0] = 100
```

会报错：

```text
TypeError
```

因为Tuple is immutable，即：元组是不可变对象（而列表是可变对象）

既然List和Tuple几乎一样、而且List还可以修改，为什么还需要Tuple呢？因为Tuple可以表示固定的数据，防止数据被误修改

Tuple也常用于多变量赋值（拆包），例如：

```python
point = (10,20)

x,y = point
```

相当于：

```python
x = 10
y = 20
```

## Dictionary（字典）

简称dict，存储键值对，有映射关系，可变

Dictionary和List最大的区别：

List通过位置访问：

```python
list[0]
```

Dictionary通过key访问：

```python
dict["key"]
```

**创建字典**：格式如下

```python
my_dict = {
    key1:value1,
    key2:value2
}
```

例如：

```python
student = {
    "name":"Tom",
    "age":20,
    "score":90
}
```

键值映射：

```text
key       value

name  ->  Tom
age   ->  20
score ->  90
```

**访问字典元素**：使用key，例如：

```python
student["name"]
```

输出：

```text
Tom
```

如果访问不存在的key，会报错：KeyError

**.get()：更安全地访问字典元素**

```python
student.get("name")
```

结果：

```text
Tom
```

如果访问不存在的key，例如：

~~~python
student.get("height")
~~~

结果：

~~~
None
~~~

不会报错

另外，如果key不存在，也可以返回默认值，例如：

```python
student.get("height", 180)
```

结果：

```
180
```

但不会把这个新的键值对加到字典里

**添加和修改元素**

字典是可变对象，里面的元素可以修改，例如把学生年龄从20改为21：

```python
student["age"] = 21
```

也可以添加新的key：

```python
student["height"] = 180
```

结果：

```python
{
"name":"Tom",
"age":21,
"score":90,
"height":180
}
```

**del：删除元素**

```python
del student["age"]
```

删除了age对应的键值对

**.pop()：删除元素并返回这个键值对中的值**

```python
student.pop("score")
```

删除score对应的键值对，并返回对应value

**直接遍历key**

```python
student = {
    "name":"Tom",
    "age":20
}

for key in student:
    print(key)
```

输出：

```text
name
age
```

**.values()：遍历value**

```python
for value in student.values():
    print(value)
```

输出：

```text
Tom
20
```

**.items()：同时遍历key和value**

```python
for key,value in student.items():
    print(key,value)
```

输出：

```text
name Tom
age 20
```

**Dictionary嵌套**：字典里也可以保存各种数据结构，例如：

```python
model_config = {
    "model":"resnet",
    "training":{
        "batch_size":32,
        "lr":0.001
    }
}
```

访问：

```python
model_config["training"]["lr"]
```

输出：

```text
0.001
```

## Set（集合）

保存多个元素，无序，元素不能重复，可变

**创建集合**：使用花括号{ }或者set( )，例如：

```python
numbers = {1,2,3}
numbers = set([1,2,3])
```

注意：空集合不能写{ }，因为它表示的是空字典。空集合应写为：

```python
empty_set = set()
```

**Set自动去重**

集合中的元素不能重复，如果有重复的元素会自动去掉多余的，例如：

```python
numbers = {1,2,2,3,3}
```

结果：

```text
{1,2,3}
```

常用于去除重复数据

**集合运算**：支持数学中的集合操作，例如现在给出集合a和b：

~~~python
a={1,2,3}
b={3,4,5}
~~~

- 并集：两个集合中的所有元素

```python
a | b
```

结果：

```text
{1,2,3,4,5}
```

- 交集：两个集合中的共同元素

```python
a & b
```

结果：

```text
{3}
```

- 差集：a中有而b中没有的元素

```python
a - b
```

结果：

```text
{1,2}
```
