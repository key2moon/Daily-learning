代码来自《深度学习入门：基于Python的理论与实现》（斋藤康毅）
基于markdown整理代码，使程序可读性更高

# chap 01 Python入门

## 1.3 Python 解释器

```bash
$ python --version
Python 3.4.1 :: Anaconda 2.1.0 (x86_64)
```

```bash
$ python#亦可输入python3,针对当前的版本而定
Python 3.4.1 |Anaconda 2.1.0 (x86_64)| (default, Sep 10 2014, 17:24:09)
[GCC 4.2.1 (Apple Inc. build 5577)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

```python
>>> 1 + 2
3
```

### 1.3.1 算数计算

```python
>>> 1 - 2 
-1
>>> 4 * 5 # *表示乘法
20
>>> 7 / 5 # /表示除法
1.4
>>> 3 ** 2# **表示乘方（3**2 3的2次方）
9
# 另外，在Python 2.x 中，整数除以整数的结果是整数，比如 7 ÷ 5 的结果是 1。
#但在Python 3.x 中，整数除以整数的结果是小数（浮点数）。
```

### 1.3.2 数据类型

```python
>>> type(10)
<class 'int'> # int 类型（整型）
>>> type(2.718)
<class 'float'> # 2.718 是 float 类型（浮点型）
>>> type("hello")
<class 'str'> # "hello" 是 str （字符串）类型
```

### 1.3.3 变量

Python 是属于“动态类型语言”的编程语言，所谓动态，是指变量的类型是根据情况自动决定的。
在上面的例子中，用户并没有明确指出“ x 的类型是 int（整型）”，是 Python 根据 x 被初始化为 10，从而判断出 x 的类型为int 的。此外，我们也可以看到，整数和小数相乘的结果是小数（数据类型的自动转换）。

```python
>>> x = 10 # 初始化
>>> print(x) # 输出 x
10
>>> x = 100 # 赋值
>>> print(x)
100
>>> y = 3.14
>>> x * y
314.0
>>> type(x * y)
<class 'float'>
```

### 1.3.4 列表

元素的访问是通过 a[0] 这样的方式进行的。[] 中的数字称为索引（下标），索引从 0 开始（索引 0 对应第一个元素）

```python
>>> a = [1, 2, 3, 4, 5] # 生成列表
>>> print(a) # 输出列表的内容
[1, 2, 3, 4, 5]
>>> len(a) # 获取列表的长度
5
>>> a[0] # 访问第一个元素的值
1
>>> a[4]
5
>>> a[4] = 99 # 赋值
>>> print(a)
[1, 2, 3, 4, 99]
```

此外，Python 的列表提供了切片（slicing）这一便捷的标记法。进行列表的切片时，需要写成 a[0:2] 这样的形式。 a[0:2] 用于取出从索引为 0 的元素到索引为 2 的元素的前一个元素之间的元素。另外，索引 −1 对应最后一个元素，−2 对应最后一个元素的前一个元素。

```python
>>> print(a)
[1, 2, 3, 4, 99]
>>> a[0:2] # 获取索引为 0 到 2 （不包括 2 ！）的元素
[1, 2]
>>> a[1:] # 获取从索引为 1 的元素到最后一个元素
[2, 3, 4, 99]

>>> a[:3] # 获取从第一个元素到索引为 3 （不包括 3 ！）的元素
[1, 2, 3]
>>> a[:-1] # 获取从第一个元素到最后一个元素的前一个元素之间的元素
[1, 2, 3, 4]
>>> a[:-2] # 获取从第一个元素到最后一个元素的前二个元素之间的元素
[1, 2, 3]
```

### 1.3.5 字典

列表根据索引，按照 0, 1, 2, . . . 的顺序存储值，而字典则以键值对的形式存储数据。字典就像《新华字典》那样，将单词和它的含义对应着存储起来。

```python
>>> me = {'height':180} # 生成字典
>>> me['height'] # 访问元素
180
>>> me['weight'] = 70 # 添加新元素
>>> print(me)
{'height': 180, 'weight': 70}
```

### 1.3.6 布尔型

Python 中有 bool 型。 bool 型取 True 或 False 中的一个值。针对 bool 型的运算符包括 and 、 or 和 not （针对数值的运算符有 + 、 - 、 * 、 / 等，根据不同的数据类型使用不同的运算符）。

```python
>>> hungry = True  # 饿了？
>>> sleepy = False # 困了？
>>> type(hungry)
<class 'bool'>
>>> not hungry
False
>>> hungry and sleepy # 饿并且困
False
>>> hungry or sleepy  # 饿或者困
True
```

### 1.3.7 if语句

```python
>>> hungry = True
>>> if hungry:
...        print("I'm hungry")
...
I'm hungry
>>> hungry = False
>>> if hungry:
...        print("I'm hungry") # 使用空白字符进行缩进
... else:
...        print("I'm not hungry")
...        print("I'm sleepy")
...
I'm not hungry
I'm sleepy
```

***Python中的空白字符具有重要的意义。***
上面的 if 语句中， if hungry: 下面的语句开头有4个空白字符。它是缩进的意思，表示当前面的条件（ if hungry ） 成立时，此处的代码会被执行。这个缩进也可以用 tab 表示，Python 中推荐使用空白字符。

### 1.3.8 for 语句

```python
>>> for i in [1, 2, 3]:
...     print(i)
...
1
2
3
```

### 1.3.9 函数

```python
>>> def hello():
...     print("Hello World!")
...
>>> hello()
Hello World!
 # 此外，函数可以取参数。
>>> def hello(object):
...     print("Hello " + object + "!")
...
>>> hello("cat")
Hello cat!
```

关闭 Python 解释器时，Linux 或 Mac OS X 的情况下输入 Ctrl-D （按住Ctrl，再按 D 键）；Windows 的情况下输入 Ctrl-Z，然后按 Enter 键。

## 1.4 Python 脚本文件

### 1.4.2 类

前面我们了解了 int 和 str 等数据类型（通过 type() 函数可以查看对象的类型）。这些数据类型是“内置”的数据类型，是 Python 中一开始就有的数据类型。
现在，我们来定义新的类。如果用户自己定义类的话，就可以自己
创建数据类型。此外，也可以定义原创的方法（类的函数）和属性。

```python
 # Python 中使用 class 关键字来定义类，类要遵循下述格式（模板）。
class 类名：
def __init__(self, 参数 , …): # 构造函数
...
def 方法名 1(self, 参数 , …): # 方法 1
...
def 方法名 2(self, 参数 , …): # 方法 2
...
```

```python
 # man.py
class Man:
    def __init__(self,name):
        self.name = name
        print("Initialized!")

    def hello(self):
        print("Hello"+self.name+"!")

    def goodbye(self):
        print("Goodbye"+self.name+"!")

m = Man("David")
m.hello()
m.goodbye()
 # 注意空格缩进四个一组
```

这里我们定义了一个新类 Man 。上面的例子中，类 Man 生成了实例（对象） m 。
类 Man 的构造函数（初始化方法）会接收参数 name ，然后用这个参数初始化实例变量 self.name 。实例变量是存储在各个实例中的变量。Python 中可以像 self.name 这样，通过在 self 后面添加属性名来生成或访问实例变量。

## 1.5 NumPy

### 1.5.1 导入NumPy

```python
>>> import numpy as np
 # 可通过np调用Numpy
```

### 1.5.2 生成NumPy数组

```python
>>> x = np.array([1.0, 2.0, 3.0])
>>> print(x)
[ 1. 2. 3.]
>>> type(x)
<class 'numpy.ndarray'>
```

### 1.5.3 NumPy 的算术运算

```python
>>> x = np.array([1.0, 2.0, 3.0])
>>> y = np.array([2.0, 4.0, 6.0])
>>> x + y # 对应元素的加法
array([ 3., 6., 9.])
>>> x - y
array([ -1., -2., -3.])
>>> x * y # 对应元素的乘法
array([ 2., 8., 18.])
>>> x / y
array([ 0.5, 0.5, 0.5])
```

> 这里需要注意的是，数组 x 和数组 y 的元素个数是相同的（两者均是元素个数为 3 的一维数组）。
> 当 x 和 y 的元素个数相同时，可以对各个元素进行算术运算。
> 如果元素个数不同，程序就会报错。

```python
>>> x = np.array([1.0, 2.0, 3.0])
>>> x / 2.0
array([ 0.5, 1. , 1.5])
# 在 NumPy 数组的各个元素和标量之间进行运算，称为广播
```

### 1.5.4 NumPy 的 N 维数组

```python
>>> A = np.array([[1, 2], [3, 4]])
 # 这里生成了一个 2 × 2 的矩阵 A 。
>>> print(A)
[[1 2]
[3 4]]
>>> A.shape
 # 矩阵 A 的形状可以通过 shape 查看
(2, 2)
>>> A.dtype
 # 矩阵元素的数据类型可以通过 dtype 查看
dtype('int64'
```

矩阵的算术运算

```python
>>> B = np.array([[3, 0],[0, 6]])
>>> A + B
array([[ 4, 2],
[ 3, 10]])
>>> A * B
array([[ 3, 0],
[ 0, 24]])

>>> print(A)
[[1 2]
[3 4]]
>>> A * 10
array([[ 10, 20],
[ 30, 40]])
```

### 1.5.5 广播

![1](/home/moon/Documents/python/pics/1.png)

```python
>>> A = np.array([[1, 2], [3, 4]])
>>> B = np.array([10, 20])
>>> A * B
array([[ 10, 40],
[ 30, 80]])
```

![2](/home/moon/Documents/python/pics/2.png)

### 1.5.6 访问元素

索引

```python
>>> X = np.array([[51, 55], [14, 19], [0, 4]])
>>> print(X)
[[51 55]
[14 19]
[ 0 4]]
>>> X[0]
# 第 0 行
array([51, 55])
>>> X[0][1] # (0,1) 的元素
55
```

for语句

```python
>>> for row in X:
...
print(row)
...
[51 55]
[14 19]
[0 4]
```

数组

```python
>>> X = X.flatten() # 将 X 转换为一维数组
>>> print(X)
[51 55 14 19 0 4]
>>> X[np.array([0, 2, 4])] # 获取索引为 0、2、4 的元素
array([51, 14, 0])
```

运用数组标记法，可以获取满足一定条件的元素。
例如，要从 X 中抽出大于 15 的元素：

```python
>>> X > 15
 # 对 NumPy 数组使用不等号运算符等（上例中是 X > 15 ） , 结果会得到一个布尔型的数组。
array([ True, True, False,
>>> X[X>15]
array([51, 55, 19])
```

> Python 等动态类型语言一般比 C 和 C++ 等静态类型语言（编译型语言）运算速度慢。实际上，如果是运算量大的处理对象，用 C/C++ 写程序更好。为此，当 Python 中追求性能时，人们会用 C/C++ 来实现处理的内容。Python 则承担“中间人”的角色，负责调用那些用 C/C++ 写的程序。NumPy 中，主要的处理也都是通过 C 或 C++ 实现的。
> 因此，我们可以在不损失性能的情况下，使用 Python 便利的语法。

## 1.6 Matplotlib

### 1.6.1 绘制简单图形

```python
import numpy as np
import matplotlib.pyplot as plt
 # 生成数据
x = np.arange(0, 6, 0.1) 
 # 使用 NumPy 的 arange 方法生成了 [0, 0.1, 0.2, ..., 5.8, 5.9] 的数据，将其设为 x
y = np.sin(x)
 # 对 x 的各个元素，应用 NumPy 的 sin 函数 np.sin()，得到 y
plt.plot(x, y)
plt.show()
 # 绘制图形
```

![3](/home/moon/Documents/python/pics/3.png)

### 1.6.2 pyplot的功能

```python
import numpy as np
import matplotlib.pyplot as plt

# 生成数据
x = np.arange(0, 6, 0.1) # 以 0.1 为单位，生成 0 到 6 的数据
y1 = np.sin(x)
y2 = np.cos(x)

# 绘制图形
plt.plot(x, y1, label="sin")
plt.plot(x, y2, linestyle = "--", label="cos") # 用虚线绘制
plt.xlabel("x") # x 轴标签
plt.ylabel("y") # y 轴标签
plt.title('sin & cos') # 标题
plt.legend()
plt.show()
```

![4](/home/moon/Documents/python/pics/4.png)

### 1.6.3 显示图像

```python
import matplotlib.pyplot as plt
from matplotlib.image import imread
img = imread('lena.png') # 读入图像（设定合适的路径！
plt.imshow(img)
plt.show()
```

> 这里，我们假定图像 lena.png 在当前目录下。读者根据自己的环境，可能需要变更文件名或文件路径。另外，本书提供的源代码中，在 dataset 目录下有样本图像 lena.png 。比如，在通过 Python 解释器从 ch01 目录运行上述代码的情况下，将图像的路径 'lena.png' 改为 '../dataset/lena.png' ，即可正确运行。
