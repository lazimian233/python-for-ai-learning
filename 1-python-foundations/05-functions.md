# 函数（Functions）



**什么是函数**

函数是一段封装起来、可以重复执行的代码

优点：减少重复代码；提高代码可读性；方便维护

**定义函数**

Python使用 def 定义函数，格式如下：

```python
def function_name():
    code
```

例如：

```python
def hello():
    print("Hello")
```

**调用函数**

调用：

```python
hello()
```

输出：

```text
Hello
```

```text
定义函数
    |
    ↓
保存代码

调用函数
    |
    ↓
执行代码
```

**函数参数**

函数可以接收外部传入的数据，例如：

```python
def hello(name):
    print("Hello", name)
```

调用：

```python
hello("Tom")
```

输出：

```text
Hello Tom
```

这里的name是形参（parameter）

而调用时传入的"Tom"是实参（argument）

如果有多个参数的话，则按照位置一一对应，例如：

```python
def add(a,b):
    print(a+b)
```

调用：

```python
add(3,5)
```

参数按照位置对应，相当于：

```python
a = 3
b = 5
```

**返回值（Return）**

目前的函数：

```python
def add(a,b):
    print(a+b)
```

只是打印结果

如果想让程序继续使用结果，就需要把结果return，例如：

```python
def add(a,b):
    return a+b
```

调用：

```python
result = add(3,5)
```

返回的结果是8，所以现在result=8

如果函数没有显式写出 return，默认返回 None

**Python支持返回多个值**

例如：

```python
def calculate(a,b):
    return a+b, a-b
```

python会自动创建tuple，实际上它就等价于：

```python
	return (a+b, a-b)
```

调用：

```python
result = calculate(10,5)
```

返回：

```python
(15,5)
```

返回的是元组。也可以拆包：

```python
add_result, sub_result = calculate(10,5)
```

相当于：

```python
add_result = 15
sub_result = 5
```

**默认参数（Default Parameters）**

函数参数可以设置默认值，当没有实参传入时，形参就会保持默认值，例如：

```python
def hello(name="User"):
    print("Hello",name)
```

调用：

```python
hello()
```

输出：

```text
Hello User
```

当有实参传入时，它就会覆盖默认参数，例如：

```python
hello("Tom")
```

输出：

```text
Hello Tom
```

**关键字参数（Keyword Arguments）**

调用函数时，可以指定实参对应的形参，例如：

```python
def student(name,age):
    print(name,age)
```

普通调用：

```python
student("Tom",20)
```

按照位置一一对应：

```text
name = Tom
age = 20
```

关键字调用：

```python
student(age=20,name="Tom")
```

这样实参的顺序就可以改变了

**参数传递**

Python中参数传递，传递的是对象的引用

- 不可变对象：通常不会改变原对象，例如int

```python
def change(x):
    x = 100

a = 10

change(a)

print(a)
```

输出：

```text
10
```

- 可变对象：可能改变原对象，例如list

```python
def add_item(lst):
    lst.append(4)


numbers=[1,2,3]

add_item(numbers)

print(numbers)
```

输出：

```text
[1,2,3,4]
```

| 类型                   | 可变性 | 函数中修改是否影响外部 |
| ---------------------- | ------ | ---------------------- |
| int,float,string,tuple | 不可变 | 通常不会               |
| list,dict,set          | 可变   | 会                     |

~~~
关于参数传递的补充：
先理解变量到底是什么。比如说a=10
在很多语言里是：创建一个变量盒子a，把数字10放进去
但在python里更像是：创建一个对象10，让变量名a指向这个对象
所以python变量本质上是：指向对象的引用
现在我们创建了一个对象，实参指向这个对象
当进行参数传递时，形参就会指向实参所指的对象，现在它们都指向同一个对象
若对象可变，并且在函数内部对该对象进行了原地修改，函数中的修改就会影响外部了
若对象不可变，通常无法修改对象本身，重新赋值时会创建一个新的对象，让形参指向这个新对象，而实参仍然指向原对象，这样函数中的修改就不会影响外部
~~~

**变量作用域（Scope）**

变量的存在范围不同，主要分为：

- 局部变量（local variable）：函数内部定义，只能在函数内使用

```python
def test():
    x=10
```

- 全局变量（global variable）：函数外定义，函数可以访问它

```python
x=10

def test():
    print(x)
```

一般尽量少使用全局变量，因为会让代码难以维护

**Lambda函数**

匿名函数（anonymous function），用于创建简单函数

普通函数：

```python
def square(x):
    return x*x
```

Lambda：

```python
square = lambda x:x*x
```

调用：

```python
square(5)
```

结果：

```text
25
```

再例如：

```python
add = lambda a,b:a+b
```

形式：

~~~
函数名 = lambda 形参:返回的结果（只能包含一个表达式）
~~~

***args：接收多个位置的参数**

有时不确定函数需要多少参数，可以使用*args来接收不固定数量的多个参数，例如：

```python
def add(*args):
    print(args)
```

调用：

```python
add(1,2,3)
```

结果：

```text
(1,2,3)
```

使用 *args后，所有额外的位置参数会被收集成一个 tuple

** **kwargs：接收多个关键字参数**

例如：

```python
def show(**kwargs):
    print(kwargs)
```

调用：

```python
show(name="Tom",age=20)
```

结果：

```text
{
"name":"Tom",
"age":20
}
```

使用 **kwargs 后，所有额外的关键字参数会被收集成一个 dictionary

**函数和方法的区别**

函数：

```python
len("Python")
```

方法：

```python
"Python".upper()
```

它们的区别：

- 函数：独立存在
- 方法：属于某个对象，通过 `对象.方法()` 调用