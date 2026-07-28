# 面向对象编程（Object-Oriented Programming，OOP）



## 面向过程和面向对象

- 面向过程：把问题拆成一个个步骤，然后写函数执行
- 面向对象：把问题拆成一个个对象，让对象自己完成任务

|                  | 面向过程编程（Procedural Programming） | 面向对象编程（Object-Oriented Programming）    |
| ---------------- | -------------------------------------- | ---------------------------------------------- |
| **核心思想**     | 关注**事情执行的步骤**                 | 关注**有哪些对象，以及对象负责什么**           |
| **思考方式**     | “我要完成这个任务，需要哪些步骤？”     | “这个系统中有哪些对象？对象有什么属性和行为？” |
| **核心单位**     | 函数（Function）                       | 类（Class）和对象（Object）                    |
| **数据**         | 数据和处理数据的函数通常分开           | 数据和操作数据的方法封装在一起                 |
| **代码组织方式** | 按功能划分函数                         | 按对象划分类                                   |
| **执行流程**     | 按代码顺序一步步执行                   | 对象之间相互调用完成任务                       |
| **关注重点**     | “怎么做（How）”                        | “谁来做（Who）”                                |
| **适合场景**     | 小型程序、简单脚本、算法流程           | 大型项目、复杂系统、框架开发                   |
| **代码复用方式** | 复制函数、调用函数                     | 继承、组合、多态                               |
| **典型语言**     | C                                      | Python、Java、C++                              |

> 面向对象编程的核心单位是类和对象

## 对象（Object）

例如，现实世界中的一个学生

```text
学生对象

属性：
- 姓名
- 年龄

行为：
- 学习
- 考试
```

对应到Python中：

```python
student.name
student.age

student.study()
student.exam()
```

对象由两部分组成：属性和方法

**属性（Attribute）**：对象的数据，例如：

```python
student.name
student.age
```

**方法（Method）**：对象的行为，例如：

```python
student.study()
student.exam()
```

## 类（Class）

对象从哪里来呢？答案是类。类是对象的模板

例如，设计学生模板：

```python
class Student:
    （这里省略）
```

这就是一个类。然后创建学生对象：

~~~
student1 = Student()
~~~

现在：

```text
Student（类）
        |
        ↓
student1（对象）
```

**class：定义类**

```python
class ClassName:
    code
```

例如：

```python
class Student:

    def study(self):
        print("studying")
```

类名通常使用 PascalCase（大驼峰命名法），各个单词首字母大写，中间不加下划线

**创建对象**

```python
class Student:
    pass


student1 = Student()
```

这里的 Student() 叫作：实例化（Instantiation）

创建出来的 student1 叫作：实例（Instance）

类和对象的关系：类用于定义对象的结构和行为，对象是类的具体实例

```text
Class
模板

 ↓ 实例化

Object
具体对象
```

**`__init__()` 方法**

创建对象时，通常需要初始化数据

例如：学生需要姓名和年龄

```python
class Student:

    def __init__(self, name, age):
        self.name = name
        self.age = age
```

创建：

```python
student1 = Student("Tom",20)
```

现在：student1.name就是”Tom”，student1.age就是20

**self：当前对象本身**

例如：

```python
class Student:

    def study(self):
        print(self.name)
```

调用：

```
student1.study()
```

Python实际上会自动传入：

```
Student.study(student1)
```

所以这里的 self 实际上就是 student1

> 对象由属性和方法两部分组成

## 属性（Attribute）

属性分为实例属性和类属性

- 实例属性：属于对象，每个对象都不同，例如：

```python
class Student:

    def __init__(self, name):
        self.name = name        
```

~~~python
student1.name = "Tom"
student2.name = "Bob"
~~~

- 类属性：属于整个类，所有对象共享，例如：

```python
class Student:

    school = "MIT"
```

```python
student1.school = "MIT"
student2.school = "MIT"
```

## 方法（Method）

类里面定义的函数叫作方法

例如：

```python
class Student:

    def study(self):
        print("study")
```

调用：

```python
student1.study()
```

方法和普通函数的区别：方法属于对象，而普通函数是独立的，例如：

普通函数：

```python
study(student)
```

方法：

```python
student.study()
```

> 面向对象的三大特征：封装、继承、多态

## 封装（Encapsulation）

将数据和操作数据的方法放在一起，隐藏对象内部实现细节，只通过公开接口访问。例如：

- 不用面向对象，数据和函数分离：

```python
name = "Tom"
age = 20

def study(name):
    ...
```

- 面向对象，数据和方法组合在一起：

```python
class Student:

    def __init__(self,name):
        self.name=name

    def study(self):
        print(self.name,"studying")
```

## 继承（Inheritance）

一个类可以获得另一个类的属性和方法。例如：

- 父类：

```python
class Animal:

    def eat(self):
        print("eat")
```

- 子类：

```python
class Dog(Animal):
    
    （这里省略）
```

创建：

```python
dog = Dog()
```

调用：

```python
dog.eat()
```

输出：

```text
eat
```

因为Dog继承了Animal

**super( )：让子类调用父类的方法**

最常见的是在子类初始化时调用父类的初始化方法，以完成父类部分的初始化，例如：

~~~python
class Animal:

    def __init__(self, name):
        self.name = name


class Dog(Animal):

    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
~~~

**方法重写**：子类可以重新定义父类方法，例如：

```python
class Dog(Animal):

    def eat(self):
        print("dog eating")
```

调用：

```python
dog.eat()
```

输出：

```text
dog eating
```

## 多态（Polymorphism）

同一个方法，不同对象有不同表现。例如：

```python
class Dog:

    def speak(self):
        print("wang")


class Cat:

    def speak(self):
        print("miao")
```

调用：

```python
animals=[Dog(),Cat()]

for animal in animals:
    animal.speak()
```

输出：

```text
wang
miao
```

## Python中的私有属性

Python没有真正意义上的 private，但是可以使用 __ 表示私有，例如：

```python
class Student:

    def __init__(self):
        self.__score = 100
```

外部不能直接访问：

~~~python
student.__score
~~~