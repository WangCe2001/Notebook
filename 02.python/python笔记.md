# 0.一些奇奇怪怪的知识

## 1.生成器和迭代器

**迭代器：**

迭代器是一个可以记住遍历的位置的对象。迭代器对象从集合的第一个元素开始访问，直到所有的元素被访问完结束。迭代器只能往前不会后退。

迭代器有两个基本的方法：

**iter()：** 返回迭代器对象本身。

**next()：**返回容器中的下一个值。如果没有更多的元素可供迭代，则抛出 `StopIteration` 异常。



```python
>>> list=[1,2,3,4]
>>> it = iter(list)    # 创建迭代器对象
>>> print (next(it))   # 输出迭代器的下一个元素
1
>>> print (next(it))
2
>>>
```



```python
list=[1,2,3,4]
it = iter(list)    # 创建迭代器对象
for x in it:
    print (x, end=" ")
    
# 输出：1 2 3 4
```



**生成器：**

在 Python 中，使用了 **yield** 的函数被称为生成器（generator）。

**yield** 是一个关键字，用于定义生成器函数，生成器函数是一种特殊的函数，可以在迭代过程中逐步产生值，而不是一次性返回所有结果。

跟普通函数不同的是，生成器是一个返回迭代器的函数，只能用于迭代操作，更简单点理解生成器就是一个迭代器。

当在生成器函数中使用 **yield** 语句时，函数的执行将会暂停，并将 **yield** 后面的表达式作为当前迭代的值返回。

然后，每次调用生成器的 **next()** 方法或使用 **for** 循环进行迭代时，函数会从上次暂停的地方继续执行，直到再次遇到 **yield** 语句。这样，生成器函数可以逐步产生值，而不需要一次性计算并返回所有结果。

调用一个生成器函数，返回的是一个迭代器对象。

下面是一个简单的示例，展示了生成器函数的使用：

```python
def countdown(n):
    while n > 0:
        yield n
        n -= 1
 
# 创建生成器对象
generator = countdown(5)
 
# 通过迭代生成器获取值
print(next(generator))  # 输出: 5
print(next(generator))  # 输出: 4
print(next(generator))  # 输出: 3
 
# 使用 for 循环迭代生成器
for value in generator:
    print(value)  # 输出: 2 1
```

以下实例使用 yield 实现斐波那契数列：

```python
#!/usr/bin/python3
 
import sys
 
def fibonacci(n): # 生成器函数 - 斐波那契
    a, b, counter = 0, 1, 0
    while True:
        if (counter > n): 
            return
        yield a
        a, b = b, a + b
        counter += 1
f = fibonacci(10) # f 是一个迭代器，由生成器返回生成
 
while True:
    try:
        print (next(f), end=" ")
    except StopIteration:
        sys.exit()
        
# 输出结果：0 1 1 2 3 5 8 13 21 34 55
```



## 2.zip()函数

**描述：**zip() 函数用于将可迭代的对象作为参数，将对象中对应的元素打包成一个个元组，然后返回由这些元组组成的列表。

如果各个迭代器的元素个数不一致，则返回列表长度与最短的对象相同，利用 * 号操作符，可以将元组解压为列表。

**语法：**

```python
zip([iterable, ...])
iterable -- 一个或多个迭代器;
```

**返回值：**返回元组列表

示例：

```python
>>> a = [1,2,3]
>>> b = [4,5,6]
>>> c = [4,5,6,7,8]
>>> zipped = zip(a,b)     # 返回一个对象
>>> zipped
<zip object at 0x103abc288>
>>> list(zipped)  # list() 转换为列表
[(1, 4), (2, 5), (3, 6)]
>>> list(zip(a,c))              # 元素个数与最短的列表一致
[(1, 4), (2, 5), (3, 6)]

>>> a1, a2 = zip(*zip(a,b))          # 与 zip 相反，zip(*) 可理解为解压，返回二维矩阵式
>>> list(a1)
[1, 2, 3]
>>> list(a2)
[4, 5, 6]
>>>
```

**参考链接：**https://www.runoob.com/python/python-func-zip.html



## 3.enumerate()函数

**描述：**enumerate() 函数用于将一个可遍历的数据对象(如列表、元组或字符串)组合为一个索引序列，同时列出数据和数据下标，一般用在 for 循环当中。

**语法：**

```python
enumerate(sequence, [start=0])
sequence -- 一个序列、迭代器或其他支持迭代对象。
start -- 下标起始位置的值
```

**返回值：**返回 enumerate(枚举) 对象

示例：

```python
>>> seasons = ['Spring', 'Summer', 'Fall', 'Winter']
>>> list(enumerate(seasons))
[(0, 'Spring'), (1, 'Summer'), (2, 'Fall'), (3, 'Winter')]
>>> list(enumerate(seasons, start=1))       # 下标从 1 开始
[(1, 'Spring'), (2, 'Summer'), (3, 'Fall'), (4, 'Winter')]

# for循环使用enumerate
>>> seq = ['one', 'two', 'three']
>>> for i, element in enumerate(seq):
...     print i, element
... 
0 one
1 two
2 three
```

参考链接：https://www.runoob.com/python/python-func-enumerate.html



## 4.if __name__ == "__main__":函数

示例：

```python
# example.py

def hello():
    print("Hello, world!")

if __name__ == "__main__":
    # 仅在直接运行 example.py 时会执行以下代码
    print("This is the main program.")
    hello()

# 直接运行，输出将是：
This is the main program.
Hello, world!
# 被导入，输出将是：
Hello, world!
```

**注意：**if下的代码要缩进，不然会报错

是一种保护机制，确保 Python 文件在直接运行时执行主逻辑，而在被导入时只提供模块功能，避免不必要的逻辑运行，同时方便测试和调试代码。

## 5.isinstance() 函数

**描述：**() 函数来判断一个对象是否是一个已知的类型，类似 type()。

**语法：**isinstance(object, classinfo)

**示例：**

```python
>>>a = 2
>>> isinstance (a,int)
True
>>> isinstance (a,str)
False
>>> isinstance (a,(str,int,list))    # 是元组中的一个返回 True
True

class A:
    pass
 
class B(A):
    pass
 
isinstance(A(), A)    # returns True
type(A()) == A        # returns True
isinstance(B(), A)    # returns True
type(B()) == A        # returns False
```



## 6.assert()断言函数

**描述：**Python assert（断言）用于判断一个表达式，在表达式条件为 false 的时候触发异常。

**语法：**

```python
assert expression
```

**示例：**

```python
>>> assert True     # 条件为 true 正常执行
>>> assert False    # 条件为 false 触发异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError
>>> assert 1==1    # 条件为 true 正常执行
>>> assert 1==2    # 条件为 false 触发异常
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError

>>> assert 1==2, '1 不等于 2'
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AssertionError: 1 不等于 2
>>>
```

1.将代码注释：ctrl+/

# 一.python基础语法

## 1.注释：

分为单行注释(#)和多行注释("""  """)

```python
# 单行注释，#后面最好接个空格

"""
多行注释
可写多行
"""

# 我是单行注释
print("hello world!")
```

## 2.变量定义格式：

变量名称 = 变量的值

## 3.输出函数：

1.print()

输出函数可以多份输出

```python
print(内容1,内容2,...,内容3)
```

2.默认使用print()函数时会自动换行，为了完成输出不换行的功能，需要在尾部加上end=''即可

```python
print("hello",end='')
print("world",end='')
```

![aa59dfb74f8f9d418b5169ad7cebbc1e](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/aa59dfb74f8f9d418b5169ad7cebbc1e.png)

## 4.查看数据类型：

type(被查看类型的数据)

## 5.字符串类型的不同定义方式：

```python
text1 = "双引号"
text2 = '单引号'
text3 = """三引号"""
```

三引号定义使用时，只要在三引号内就是同一字符串

```python
text = """
在三引号字符串内
全部都是
字符串
"""
```

## 6.数据类型转换：

```python
int(x)		#将x转换为一个整数
float(x)	#将x转换为一个浮点数
str(x)		#将对象x转换为字符串
```

注意：1.任何类型，都可以通过str()转换成字符串

​	    2.==字符串内必须真的是数字，才可以将字符串转换为数字==

例如：

```python
int("张三")  #这是不允许的
```

## 7.标识符命名：

只允许出现英文、中文(不推荐)、数字、下划线这四类元素

感觉和C的定义差不多

在python中的英文字母最好全小写，这是变量的命名规范

## 8.运算符：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e4db3f35618468f350cd3dde5d3c20b3.png)

## 9.字符串扩展

1)如果想要在字符串本身内部带双引号，可以使用==转移字符==\来将引号解除效用，变成配普通字符串

```python
print("\"name")
```

此时输出的是"name

2)字符串拼接

方法1：使用+

```python
print("name "+"is "+"王策")
```

![17553d491af6876a6d2b5290a98fdde1](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/17553d491af6876a6d2b5290a98fdde1.png)

但是+无法完成字符串和数字的拼接，只能完成==字符串和字符串的拼接==

```python
# 下面的就是不被允许的
print("name"+10)
```

方法2L:字符串的格式化

```python
# 使用%s来完成字符串的占位
print("我的名字是%s" % "张三")
```

![8e2d7ab3bcdad4e0677ca471d547455e](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/8e2d7ab3bcdad4e0677ca471d547455e.png)

```python
# 一句里有多个字符串需要占位时，需要加括号
name1 = "张三"
name2 = "李四"
print("我的名字是:%s,他的名字是%s" % (name1,name2))
```

注意后面的==%前面不需要加逗号来断句==

![6a548556f5130c2bf2896a4ec97020f4](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/6a548556f5130c2bf2896a4ec97020f4.png)

```python
# 多种数据类型占位使用方法：
name = "传智博客"
year = 2006
price = 19.99
print("我是：%s，我成立于%d，我今天的股份是：%f" % (name,year,price))
```

![7e7d5535cd8543d192463baa0f55484f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/7e7d5535cd8543d192463baa0f55484f.png)

3)字符串格式化

我们可以使用辅助符号m.n来控制数据的宽度和精度

示例：

```python
num1 = 11
num2 = 11.345
print("数字11宽度限制5,结果：%5d" % num1)
print("数组11宽度限制1，结果：%1d" % num1)
print("数字11.345宽度限制7，小数精度2，结果：%7.2f" % num2)
print("数字11.345不限制宽度，小数精度2，结果：%.2f" % num2)
```

![20aa4bc18e834ca4cfb6c36c10be8934](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/20aa4bc18e834ca4cfb6c36c10be8934.png)

在限制中m或n都可以省略；如果==m比式子本身宽度还小，则m不生效==；.n会对小数部分做精度限制，同时==四舍五入==；小数点也算一位，==缺的位置会用空格补全==

4）字符串的快速写法：

f"{变量}{变量}"

```python
name = "张三"
year = 2006
price = 19.99
print(f"我是{name},成立于{year},价格是{price}")
```

![14c2dabfbc0ff44f1a61a78ef1bd0a3f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/14c2dabfbc0ff44f1a61a78ef1bd0a3f.png)

## 10.input()输入语句

1.使用一个变量接受(存储)input语句获取的键盘输入数据即可

2.使用input语句输入的数据系统都会==默认存储为字符串==，==如果想要将其变为整数，需要强制转换==

```python
name = input("请输入您的名字")
print("您的名字是：%s" % name)
```

![7b9f8425da51e9ad70004eda6963a9d4](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/7b9f8425da51e9ad70004eda6963a9d4.png)

3.在input()函数内部加入字符串语句的效果，和在input语句之上加入print语句相同

第一章练习1：

![add31b7b14d5a198bfb28d40d0e78971](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/add31b7b14d5a198bfb28d40d0e78971.png)

```python
name = "传智博客"           # 公司名
stock_price = 19.99       # 当前股价
stock_code = "003032"     # 股票代码
stock_price_daily_growth_factor = 1.2   # 股票每日增长系数
growth_days = 7     #增长天数
print(f"公司：{name},股票代码：{stock_code},当前股价：{stock_price}")
print("每日增长系数是：%.1f,经过%d天的增长后，股价达到了：%.2f" % (stock_price_daily_growth_factor,growth_days,stock_price*stock_price_daily_growth_factor**growth_days))

```

![68a95b7851275bba9e51111a53a7d45d](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/68a95b7851275bba9e51111a53a7d45d.png)

注意：使用%s %d这种多个占位时，需要在后面使用括号()将所用数据全部包含

# 二.python判断语句

## 1.布尔类型与比较运算符

1.布尔类型字面量：

true——真

flase——假

2.比较运算符

![27e11b4556bb557f5e7168cd8614b503](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/27e11b4556bb557f5e7168cd8614b503.png)

## 2.if语句

### 2.1 if语句

1.使用if语句时，需要在if后加==冒号==:

2.if语句下缩进==4个空格==的代码块，是if判断后的执行语句

```python
print("欢迎来到游乐场，儿童免费，成人收费。")
age = input("请输入您的年龄：")
age = int(age)
if age >= 18:
    print("您已成年，游玩需要补票10元.")
print("祝您游玩愉快")
```

![b60a1b654fefd90832ed63bb3969b8db](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/b60a1b654fefd90832ed63bb3969b8db.png)

### 2.2 if else组合语句

```python
print("欢迎来到游乐场")
height = int(input("请输入您的身高："))
if height >= 120:
    print("您的身高超出120cm，游玩需要补票10元.")
else:
    print("您的身份未超出120cm，可以免费游玩")
print("祝您游玩愉快")
```

注意：else后面也要加==冒号==:，下面的代码块也要==缩进四个空格==

![5e83104c957b94caec187a24920a96ca](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/5e83104c957b94caec187a24920a96ca.png)

![ce7fed16c65372ccfc15009d84e36044](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/ce7fed16c65372ccfc15009d84e36044.png)

### 2.3 if elif else语句

![36df264d8dca07c31b23763f508ee33b](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/36df264d8dca07c31b23763f508ee33b.png)



代码示例：

```python
num = 10
if int(input("请输入第一次猜想的数字：")) == num:
    print("猜对了！")
elif int(input("不对，再猜一次：")) == num:
    print("猜对了！")
elif int(input("不对，最后猜一次：")) == num:
    print("猜对了！")
else:
    print("Sorry，全部猜错了，我的的是%d" % num)
```

![3cdeead26adb1c3da897b8ad6d078983](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3cdeead26adb1c3da897b8ad6d078983.png)

![0cdf57e7f8f2e49d8fbafb606547b20a](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/0cdf57e7f8f2e49d8fbafb606547b20a.png)

注意：可以在if的判断语句中使用input和强制类型转换，方便语句操作



练习1：三次机会猜1~10之间的随机数

```python
import random
num = random.randint(1,10)
guess = int(input("请第一次输入数字："))
if guess == num:
    print("第一次就猜对了！")
elif guess < num:
    print("第一次猜的小了，请第二次重新猜")
    guess = int(input())
    if guess == num:
        print("第二次猜对了！")
    elif guess < num:
        print("第二次猜的小了，请第三次重新猜")
        guess = int(input())
        if guess == num:
            print("第三次猜对了！")
        elif guess < num:
            print("第三次猜的小了")
        elif guess > num:
            print("第三次猜的大了")
    elif guess > num:
        print("第二次猜的大了，请第三次重新猜")
        guess = int(input())
        if guess == num:
            print("第三次猜对了！")
        elif guess < num:
            print("第三次猜的小了")
            guess = int(input())
        elif guess > num:
            print("第三次猜的大了")
            guess = int(input())
elif guess > num:
    print("第一次猜的大了，请第二次重新猜")
    guess = int(input())
    if guess == num:
        print("第二次猜对了！")
    elif guess < num:
        print("第二次猜的小了，请第三次重新猜")
        guess = int(input())
        if guess == num:
            print("第三次猜对了！")
        elif guess < num:
            print("第三次猜的小了")
            guess = int(input())
        elif guess > num:
            print("第三次猜的大了")
            guess = int(input())
    elif guess > num:
        print("第二次猜的大了，请第三次重新猜")
        guess = int(input())
        if guess == num:
            print("第三次猜对了！")
        elif guess < num:
            print("第三次猜的小了")
        elif guess > num:
            print("第三次猜的大了")

print("随机数是：%d" % num)
```

![792f3785a0850d1b95b5acb288cc7593](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/792f3785a0850d1b95b5acb288cc7593.png)

## 3.与或非

与：and

或：or

非：not

| 运算符 | 逻辑表达式 | 描述                                                         | 实例                    |
| :----- | :--------- | :----------------------------------------------------------- | :---------------------- |
| and    | x and y    | 布尔"与" - 如果 x 为 False，x and y 返回 False，否则它返回 y 的计算值。 | (a and b) 返回 20。     |
| or     | x or y     | 布尔"或" - 如果 x 是非 0，它返回 x 的计算值，否则它返回 y 的计算值。 | (a or b) 返回 10。      |
| not    | not x      | 布尔"非" - 如果 x 为 True，返回 False 。如果 x 为 False，它返回 True。 | not(a and b) 返回 False |



```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
a = 10
b = 20
 
if  a and b :
   print "1 - 变量 a 和 b 都为 True"
else:
   print "1 - 变量 a 和 b 有一个不为 True"
 
if  a or b :
   print "2 - 变量 a 和 b 都为 True，或其中一个变量为 True"
else:
   print "2 - 变量 a 和 b 都不为 True"
 
# 修改变量 a 的值
a = 0
if  a and b :
   print "3 - 变量 a 和 b 都为 True"
else:
   print "3 - 变量 a 和 b 有一个不为 True"
 
if  a or b :
   print "4 - 变量 a 和 b 都为 True，或其中一个变量为 True"
else:
   print "4 - 变量 a 和 b 都不为 True"
 
if not( a and b ):
   print "5 - 变量 a 和 b 都为 False，或其中一个变量为 False"
else:
   print "5 - 变量 a 和 b 都为 True"

# 输出结果：
1 - 变量 a 和 b 都为 True
2 - 变量 a 和 b 都为 True，或其中一个变量为 True
3 - 变量 a 和 b 有一个不为 True
4 - 变量 a 和 b 都为 True，或其中一个变量为 True
5 - 变量 a 和 b 都为 False，或其中一个变量为 False
```



# 三.python循环语句

## 1.while循环

![image-20240813090545243](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813090545243.png)

while语句：while 条件 :

while语句==末尾要加上冒号==

示例：求1~100的和

```python
i = 1
num = 0
while i<=100:
    num += i
    i += 1
print("1~100的和是：%d" % num)
```

注意：while下面缩进的代码块都属于while循环内

示例2：猜1~100之间的随机数

```python
import random
num = random.randint(1,100)
guess = int(input("请输入数字："))
while guess != num:
    if guess > num:
        guess = int(input("猜大了，请重新猜"))
    else:
        guess = int(input("猜小了，请重新猜"))
print("猜对了，随机数是%d" % num)
```

![30fbd18981c329d30cfa2f6d719b88c9](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/30fbd18981c329d30cfa2f6d719b88c9.png)

## 2.while的嵌套循环

![image-20240812174230217](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240812174230217.png)



案例：

打印九九乘法表

```python
i = 0
while i<9 :
    i += 1
    j = 1
    while j <= i :
        print("%d*%d=%d\t" % (j,i,j*i),end = '')
        j += 1
    print()
```

![59c3b620c9758cfe7658802e407bfac1](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/59c3b620c9758cfe7658802e407bfac1.png)

注意：1.要想使print函数不自动换行，需要在结尾加上end=''语句

​	    2.如果想要==字符串对齐==，需要==使用制表符\t==，程序会使数据自动对齐

## 3.for循环

![image-20240813090555396](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813090555396.png)



程序中的for循环基础语法：

```python
for 临时变量 in 待处理数据集:
	循环满足条件时执行的代码
```

从待处理数据集中：==逐个取出数据==，赋值给临时变量

注意：1.for后面也要加上冒号:

​	    2.临时变量如果在for==之前没有定义==，==不建议==在for==之后==的代码块中==使用==(类似于C中的局部变量)

案例1：数一数有几个a

```python
name = "itheima is a brand of itcast"
j = 0
for i in name:
    if i == 'a':
        j += 1
print("字符串中一共有%d个a" % j)
```

![c55168e25ff46e46f022a24ff9786c89](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/c55168e25ff46e46f022a24ff9786c89.png)

## 4.range语句

range语句的功能是：获得一个数字序列

range语句的语法格式：

语法1：

```python
# 从0开始，步长为1，到num结束(不包含num本身)
range(num)
```

语法2：

```python
# 从num1开始，到num2结束(不含num2本身)
range(num1,num2)
```

语法3：

```python
# 从num1开始，到num2结束(不含num2本身)，步长以step值为准
range(num1,num2,step)
```

案例1：记录从1~100内(不包括100)有多少个偶数

```python
num = 100
count = 0
for i in range(1,num):
    if i%2 == 0:
        count += 1
print("总共有%d个偶数" % count)
```

![3998881d7f3bdf4db240f24658f82f80](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3998881d7f3bdf4db240f24658f82f80.png)

## 5.for循环的嵌套

![image-20240813095552241](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813095552241.png)

注意事项：

1.需要注意缩进，嵌套for循环同样通过缩进确定层次关系

2.for循环和while循环==可以相互嵌套使用==

案例1：九九乘法表：

```python
for i in range(9):
    i +=1
    j = 1
    for x in range(j,i+1):
        print("%d*%d=%d\t" % (j,i,j*i),end = '')
        j += 1
    print()
```

![image-20240813100108676](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813100108676.png)

## 6.循环中断：continue和break

![image-20240813100913026](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813100913026.png)

continue只能控制左图编号1的for循环对编号2的for循环，无影响

1.continue的作用是：

中断所在循环的当次执行，直接进入下一次

![image-20240813101204037](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813101204037.png)

break只能控制左图编号1的循环对编号2的循环，无影响

2.break的作用是：直接结束所在的循环

3.注意事项：

- continue和break，在for和while循环中作用一致


- 在嵌套循环中，只能作用在所在的循环上，==无法对上层循环起作用==


案例1：

![029e1ed86853595ae253979b778edd1c](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/029e1ed86853595ae253979b778edd1c.png)

```python
# 员工总工资1万元
money = 10000
# 随机生成20个员工，并用score记录每个人的随机绩效得分
for i in range(1,21):
    # 随机生成的绩效得分为1~10分
    import random
    score = random.randint(1,10)
    # 如果生成的绩效得分小于5，则不发工资
    if score < 5 :
        print("员工%d的绩效分为%d,不发工资，下一位" % (i,score))
    # 如果生成的绩效得分大于5，则发1000元
    else:
        money -= 1000
        print("员工%d的绩效分为%d,发工资1000元，账户余额还剩%d元" % (i,score,money))
    # 如果最后的money为0，则剩余的员工都不发工资
        if money == 0:
            print("钱发完了，下个月领取吧")
            break
```

# 四.python函数

## 1.函数的定义

1.函数的定义语法：

```python
def 函数名(传入参数):
    函数体
    return 返回值
```

==参数==不需要的话==可以省略==

==返回值==不需要的话==可以省略==

示例：

```python
def func():
    print("函数使用定义")
    return None
func()
```

![fbc9e3d0aebe5488c6774f4cfef007c6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/fbc9e3d0aebe5488c6774f4cfef007c6.png)

2.函数的返回值None类型：

None常用于返回值为空的场景，如果没有return语句，那么函数会自动返回一个None作为返回值，如果用于if语句，None的作用等同于false

3.函数的说明文档：使用三引号

```python
def add(x,y):
    """
    add函数可以接受2个参数，进行2数相加的功能
    :param x:形参x表示相加的其中一个数字 
    :param y:形参u表示相加的另一个数字
    :return: 返回值是两数相加的结果
    """
    result = x + y
    print(f"两数相加的结果是{result}")
    return result
add(2,4)
```

鼠标悬停在函数体上会看到函数说明

![a6ddd0886b76e5999ef7f5a77d97f300](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/a6ddd0886b76e5999ef7f5a77d97f300.png)

## 2.变量的作用域

1.函数体内部的变量一般为局部变量，函数体外部定义的变量一般是全局变量

2.在函数体内部一般是无法更改全局变量的值的

3.如果想要在函数体内部==修改全局变量==的值需要==添加global关键字==

示例：

```python
num = 100
def func1():
    print(num)
def func2():
    global num
    num = 200
    print(num)
func1()
func2()
print(f"全部变量num={num}")
```

![34b69fa42b1faa5a8b8d0171e9fe4cec](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/34b69fa42b1faa5a8b8d0171e9fe4cec.png)

如果没有global关键字，在函数体2中也是无法改变num的具体值的

## 3.函数的多返回值

![image-20240814170501852](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814170501852.png)



## 4.函数的多种传参方式

1.**位置参数**：调用函数时根据函数定义的参数位置来传递参数

![image-20240814171949689](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814171949689.png)

注意：传递的参数和定义的参数的==顺序及个数必须一致==

2.**关键字参数**：函数调用时通过=="键=值"==形式传递参数

作用：可以让函数更加清晰、容易使用，同时也清楚了参数的顺序需求

![image-20240814180800499](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814180800499.png)

注意：函数调用时，如果有位置参数时，==位置参数==必须==在关键字参数的前面==，但==关键字参数==之间==不存在先后顺序==

3.**缺省参数**：缺省参数也叫默认参数，用于定义函数，为参数提供默认值，调用函数时可不传默认参数的值(注意：所有位置参数必须出现在默认参数前，包括函数定义和调用)

作用：当调用函数时==没有传递参数==，就会==使用默认缺省参数==对应的值

![image-20240814181043958](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814181043958.png)

注意：函数调用时，如果为缺省参数传值则修改默认参数值，否则使用这个默认值

**4.不定长参数：**不定长参数也叫可变参数，用于不确定调用的时候会传递多少个参数的场景

作用：当调用函数时不确定参数个数时，可以使用不定长参数

不定长参数的类型：

**4.1 位置传递：**传进的所有参数都会被==args变量收集==，它会根据传进参数的位置合并为一个==元组(tuple)==，args是元组类型，一般用args来定义

![image-20240814181331327](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814181331327.png)

4.2 **关键字传递**：参数是=="键=值"==形式的情况下，所有的"键=值"都会被==kwargs==接受，同时根据"键=值"组成==字典==，一般用kwargs来定义

![image-20240814181443646](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814181443646.png)

## 5.函数作为参数传递

1.函数本身可以作为参数，传入另一个函数中进行使用的，这是一种==计算逻辑的传递==，而非数据的传递

![image-20240815091526643](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240815091526643.png)

## 6.lambda匿名函数的语法

1.lambda的基本语法：

```python
lambda 传入参数 : 函数体(一行代码)
```

2.匿名函数用于临时构建一个函数，只用一次的场景

3.匿名函数的定义中，函数体只能写一行代码，如果函数体要写多行代码，不可用lambda匿名函数，应使用def定义带名函数

![image-20240815092720178](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240815092720178.png)

输出结果：

![f283db53516b36be41af3a509690298f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f283db53516b36be41af3a509690298f.png)

匿名函数传入计算逻辑x+y，最后返回结果给result

# 五.python数据容器

## 1.list列表

1.list列表的基本语法：

![image-20240813143955004](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813143955004.png)

```python
name = ["hello","666","bitch"]
print(name[0])
print(name[1])
print(name[2])
```

![bec08b18344da768af38c969c54c0051](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/bec08b18344da768af38c969c54c0051.png)

2.list列表以==中括号==作为标识，列表中的每一个元素之间，用逗号隔开，可以==通过下标来搜索值==

3.列表可以一次存储多个数据，且==可以为不同的数据类型==，==支持嵌套==

4.列表的函数与功能：

| **编号** | **使用方式**            | **作用**                                       |
| -------- | ----------------------- | ---------------------------------------------- |
| 1        | 列表.append(元素)       | 向列表中追加一个元素                           |
| 2        | 列表.extend(容器)       | 将数据容器的内容依次取出，追加到列表尾部       |
| 3        | 列表.insert(下标, 元素) | 在指定下标处，插入指定的元素                   |
| 4        | del 列表[下标]          | 删除列表指定下标元素                           |
| 5        | 列表.pop(下标)          | 删除列表指定下标元素                           |
| 6        | 列表.remove(元素)       | 从前向后，删除此元素第一个匹配项               |
| 7        | 列表.clear()            | 清空列表                                       |
| 8        | 列表.count(元素)        | 统计此元素在列表中出现的次数                   |
| 9        | 列表.index(元素)        | 查找指定元素在列表的下标  找不到报错ValueError |
| 10       | len(列表)               | 统计容器内有多少元素                           |
| 11       | 列表.head(元素)         | 截取列表前n个元素；不添加数字时默认值是5       |

列表函数的具体使用方法可以翻阅手册或视频

5.列表的特点：

![image-20240814145824686](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145824686.png)

6.案例1.：

![2afb06ea217f94c81c15d01b3e8b4541](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/2afb06ea217f94c81c15d01b3e8b4541.png)

```python
# 使用中括号定义一个列表
age_list = [21,25,21,23,22,20]
print(f"初始列表是:{age_list}")
# 1.在列表尾追加一个数字31，到列表的尾部并输出
age_list.append(31)
print("1.尾部添加数字31后的列表是：%s" % age_list)
# 2.追加一个新列表[29,33,30]，到列表的尾部，并输出
add_list = [29,33,30]
age_list.extend(add_list)
print(f"2.尾部添加新列表[29,33,30]后的列表是：{age_list}")
# 3.取出第一个元素(应是：21)
print("3.第一个元素是：%d" % age_list[0])
# 4.取出最后一个元素(应是：30)
print(f"4.取出最后一个元素是：{age_list[-1]}")
# 5.查找元素31，在列表中的下标位置
print("5.元素31在列表中的下标位置是：%d" % age_list.index(31))
```

案例2：

![6fe42d9386c78cf2650dacb9c80f2433](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/6fe42d9386c78cf2650dacb9c80f2433.png)

```python
# 定义一个列表
num_list = [1,2,3,4,5,6,7,8,9,10]
# 1.使用while循环遍历出列表中的偶数并存入一个新列表中
i = 0
j = 0
new_list1 = list()
while i< len(num_list):
    if num_list[i] % 2 == 0:
        new_list1.append(num_list[i])
        j += 1
    i += 1
print(f"1.使用while循环列表中的偶数列表为：{new_list1}")
# 2.使用for循环遍历出列表中的偶数并存入一个新列表中
new_list2 = list()
for m in num_list:
    if m % 2 == 0:
        new_list2.append(m)
print(f"2.使用for循环列表中的偶数列表为：{new_list2}")
```

![f6f95d95103c4ca22ba611ec1117aa86](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f6f95d95103c4ca22ba611ec1117aa86.png)

**列表推导式：**

```python
# 列表推导式的结构为：
[表达式 for 元素 in 可迭代对象 if 条件]
```

**表达式**：对每个元素的操作，可以是直接的值、函数调用、计算结果等。

**for 元素 in 可迭代对象**：遍历可迭代对象（如列表、字符串、范围、字典等）。

**if 条件**（可选）：对每个元素进行条件判断，只有满足条件的元素才会被加入到结果列表中。

代码示例：

```python
result = [i * i for i in range(10)]
print(result)
# 输出：[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

# 只保留偶数并平方
result = [i ** 2 for i in range(10) if i % 2 == 0]
print(result)
# 输出：[0, 4, 16, 36, 64]

# 定义一个函数，用于计算平方
def square(x):
    return x ** 2

# 调用函数生成列表
result = [square(i) for i in range(10)]
print(result)
# 输出：[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```



## 2.tuple元组

1.列表是可以修改的，但是元组一旦定义完成，就==不可修改==

2.元组定义：使用的是==小括号==

![image-20240813161152897](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813161152897.png)

3.当元组内元素==只有一个时==，==需要在元素后面加上逗号==，元组也==可以存储不同的数据类型==

![image-20240813161220803](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813161220803.png)

4.元组也==支持嵌套==，元组也==可以通过下标来搜索值==

![image-20240813161240469](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813161240469.png)

5.元组的相关操作：

| **编号** | **方法**         | **作用**                                           |
| -------- | ---------------- | -------------------------------------------------- |
| 1        | 元组.index(元素) | 查找某个数据，如果数据存在返回对应的下标，否则报错 |
| 2        | 元组.count(元素) | 统计某个数据在当前元组出现的次数                   |
| 3        | len(元组)        | 统计元组内的元素个数                               |

![image-20240813161533746](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813161533746.png)

6.元组的值虽然不可以被修改，但是==元组内列表的值可以被修改==

![image-20240813161651819](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813161651819.png)

7.元组的特点：

![a66049c41375b3330a926c4aa3dd0cce](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/a66049c41375b3330a926c4aa3dd0cce.png)

8.案例：

![549390bd9983fec17068371576cea84f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/549390bd9983fec17068371576cea84f.png)、

```python
# 使用小括号来定义元组
student_tuple = ("周杰伦",11,["football","music"])
# 1.查询其年龄所在的下标位置
print(f"1.年龄所在的下标位置为{student_tuple.index(11)}")
# 2.查询学生姓名
print(f"2.学生的姓名是：{student_tuple[0]}")
# 3.删除学生爱好中的football
student_tuple[2].pop(0)
print(f"3.删除学生爱好中的football后的元组为：{student_tuple}")
# 4.增加爱好：coding到爱好list内
student_tuple[2].append("coding")
print(f"4.增加coding到list后的元组为：{student_tuple}")
```

![25044c4e09531c859c5e9d450bf6ace6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/25044c4e09531c859c5e9d450bf6ace6.png)

## 3.str字符串

1.字符串和列表、元组一样，也==可以通过下标来索引==

![image-20240813163948559](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240813163948559.png)

2.字符串函数：

| **编号** | **操作**                             | **说明**                                                     |
| -------- | ------------------------------------ | ------------------------------------------------------------ |
| 1        | 字符串[下标]                         | 根据下标索引取出特定位置字符                                 |
| 2        | 字符串.index(字符串）                | 查找给定字符的第一个匹配项的下标                             |
| 3        | 字符串.replace(字符串1, 字符串2)     | 将字符串内的全部字符串1，替换为字符串2  不会修改原字符串，==而是得到一个新的== |
| 4        | 字符串.split(字符串)                 | 按照给定字符串，对字符串进行分隔  不会修改原字符串，==而是得到一个新的**列表**== |
| 5        | 字符串.strip()  字符串.strip(字符串) | 移除首尾的空格和换行符或指定字符串，==得到一个**字符串**==   |
| 6        | 字符串.count(字符串)                 | 统计字符串内某字符串的出现次数                               |
| 7        | len(字符串)                          | 统计字符串的字符个数                                         |

具体功能参考视频与手册

3.字符串内==只可以存储字符==，并且字符串==一经确认将不可更改==，如果想得到改动的字符串，那么需要一个新的变量来接受改变后的字符串

4.字符串的特点：

![image-20240814145558240](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145558240.png)

5.案例：

![1cd8a6cd4d14aedad738ba34741533e2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1cd8a6cd4d14aedad738ba34741533e2.png)

```python
# 给定一个字符
str = "itheima itcast boxuegu"
# 1.统计字符串内有多少个"it"字符
print(f"1.字符串内共有{str.count("it")}个it字符")
# 2.将字符内的空格，全部替换为字符：“|”
new_str1 = str.replace(" ","|")
print(f"2.将空格全部替换后的字符串为：{new_str1}")
# 3.并按照"|"进行字符串分割，得到列表
new_str2 = new_str1.split("|")
print(f"3.按照字符|切割后的字符串为：{new_str2}")
```

![b5fee476d224563105169178cf3fcdac](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/b5fee476d224563105169178cf3fcdac.png)

## 4.序列

1.序列是指：内容连续、有序，可使用下标索引的一类数据容器

列表、元组、字符串，均可以视为序列

![image-20240814133641296](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814133641296.png)

![image-20240814133645432](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814133645432.png)

2.序列的语法：

```python
序列[起始下标:结束下标:步长]
# 1.起始下标表示从何处开始，可以留空，留空视作从头开始
# 2.结束下标(不含)表示何处结束，可以留空，留空视作截取到结尾
# 3.步长表示，依次去元素的间隔，步长为正正向取，步长为负负向取(反向取时起始下标和结束下标也要反向标记)
```

表示从序列的指定位置开始，依次取出元素，到指定位置结束(==不包含结束位置的元素==)，得到一个新序列

注意：此操作==不会影响序列本身==，而是会==得到一个新的序列==(列表、元组、字符串)

3.案列：

![41860c5c6284076dbaa188e59a5889f2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/41860c5c6284076dbaa188e59a5889f2.png)

```python
# 1.新建一个字符串
str = "万过薪月，员序程马黑来，nohtyP学"
"""
2.由于字符串是一个序列，所以可以通过序列的反向切片得到一个新序列
3.为了得到黑马程序员，设置步长为-1，起始点为-10，终止点为-15（不包含最后一位）
"""
new_str = str[-10:-15:-1]
# 4.输出新的字符串
print(f"新的字符串为：{new_str}")
```

![7970b00e797caff0f7f17ba54edaca6c](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/7970b00e797caff0f7f17ba54edaca6c.png)

## 5.set集合

1.集合的特点：==不支持元素的重复==(==自带去重功能==)，并且==内容无序==

2.集合==不支持下标索引访问==，所以集合也不支持while循环

3.集合的定义：使用==大括号==

![image-20240814140357514](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814140357514.png)

4.集合的函数功能：

| **编号** | **操作**                       | **说明**                                                    |
| -------- | ------------------------------ | ----------------------------------------------------------- |
| 1        | 集合.add(元素)                 | 集合内添加一个元素                                          |
| 2        | 集合.remove(元素)              | 移除集合内指定的元素                                        |
| 3        | 集合.pop()                     | 从集合中随机取出一个元素                                    |
| 4        | 集合.clear()                   | 将集合清空                                                  |
| 5        | 集合1.difference(集合2)        | 得到一个新集合，内含2个集合的差集  原有的2个集合内容不变    |
| 6        | 集合1.difference_update(集合2) | 在集合1中，删除集合2中存在的元素  集合1被修改，集合2不变    |
| 7        | 集合1.union(集合2)             | 得到1个新集合，内含2个集合的全部元素  原有的2个集合内容不变 |
| 8        | len(集合)                      | 得到一个整数，记录了集合的元素数量                          |

5.集合的特点：

![image-20240814145512034](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145512034.png)

6.案例：

![27f4f79b0e29187d26abcd7782826f7f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/27f4f79b0e29187d26abcd7782826f7f.png)

```python
# 1.新建一个列表对象：
my_list = ["黑马程序员","传智播客","黑马程序员","传智播客","itheima","itcast","itheima","itcast"]
# 2.定义一个空集合
my_set = set()
# 3.通过for循环遍历列表,将在for循环中将列表的元素添加至集合
for i in my_list:
    my_set.add(i)
# 4.输出最后的集合
print(f"最后的集合为：{my_set}")
```

![e4b93574737aaa7d50821629a13a1829](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e4b93574737aaa7d50821629a13a1829.png)

## 6.dict字典

1.字典的定义：

![image-20240814143920767](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814143920767.png)

字典使用==大括号{}==存储原始，每一个元素是一个键值对，每一个键值对包含Key和Value，==用冒号分隔==，==键值对之间使用逗号分隔==

2.Key和Value可以是任意类型的数据(key不可为字典)

3.==Key不可重复==，重复会对原有数据覆盖

4.字典同集合一样，==不可以使用下标索引==，但是字典可以通过Kry值来取得对应的Value，使用key==索引时使用中括号==

5.字典在定义时是可以嵌套的

![image-20240814145219624](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145219624.png)

对嵌套的字典的内容获取过程如下：

![image-20240814145252997](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145252997.png)

6.字典的功能：

| **编号** | **操作**          | **说明**                                      |
| -------- | ----------------- | --------------------------------------------- |
| 1        | 字典[Key]         | 获取指定Key对应的Value值                      |
| 2        | 字典[Key] = Value | 添加或更新键值对                              |
| 3        | 字典.pop(Key)     | 取出Key对应的Value并在字典内删除此Key的键值对 |
| 4        | 字典.clear()      | 清空字典                                      |
| 5        | 字典.keys()       | 获取字典的全部Key，可用于for循环遍历字典      |
| 6        | len(字典)         | 计算字典内的元素数量                          |

7.字典的特点：

![image-20240814145434116](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240814145434116.png)

8.案例：

![520ed43241f49bb24ad95e6b9eb93d7e](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/520ed43241f49bb24ad95e6b9eb93d7e.png)

```python
# 1.生成员工信息字典：
student_dict = {
    "王力宏": {"部门": "科技部", "工资": 3000, "级别": 1},
    "周杰伦": {"部门": "市场部", "工资": 5000, "级别": 2},
    "林俊杰": {"部门": "市场部", "工资": 7000, "级别": 3},
    "张学友": {"部门": "科技部", "工资": 4000, "级别": 1},
    "刘德华": {"部门": "市场部", "工资": 6000, "级别": 2}
}
# 2.输出当前员工信息
print(f"当前员工信息如下：{student_dict}")
# 3.通过for循环，对所有级别为1级的员工，级别上升1级，薪水增加1000元
for name in student_dict:
    if  student_dict[name]["级别"] == 1:
        student_dict[name]["级别"] = 2
        student_dict[name]["工资"] += 1000
# 3.输出修改后的员工信息
print(f"修改后的员工信息如下：{student_dict}")
```

![9a48b9e0eafe2c0a3f8fb746526d7778](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/9a48b9e0eafe2c0a3f8fb746526d7778.png)

## 7.数据容器对比总结

1.各个容器的特点对比：

|          | **列表**                         | **元组**                           | **字符串**         | **集合**               | **字典**                                           |
| -------- | -------------------------------- | ---------------------------------- | ------------------ | ---------------------- | -------------------------------------------------- |
| 元素数量 | 支持多个                         | 支持多个                           | 支持多个           | 支持多个               | 支持多个                                           |
| 元素类型 | 任意                             | 任意                               | 仅字符             | 任意                   | Key：Value  Key：除字典外任意类型  Value：任意类型 |
| 下标索引 | 支持                             | 支持                               | 支持               | 不支持                 | 不支持                                             |
| 重复元素 | 支持                             | 支持                               | 支持               | 不支持                 | 不支持                                             |
| 可修改性 | 支持                             | 不支持                             | 不支持             | 支持                   | 支持                                               |
| 数据有序 | 是                               | 是                                 | 是                 | 否                     | 否                                                 |
| 使用场景 | 可修改、可重复的一批数据记录场景 | 不可修改、可重复的一批数据记录场景 | 一串字符的记录场景 | 不可重复的数据记录场景 | 以Key检索Value的数据记录场景                       |
| 括号     | 中括号[]定义                     | 小括号()定义                       | 双/单/三引号       | 大括号{}               | {键值对}                                           |

2.各个容器的适用场景：

![be3f2c9b593860445b2d09678c931d2f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/be3f2c9b593860445b2d09678c931d2f.png)

## 8.容器通用功能

1.容器的通用功能表：

| **功能**                     | **描述**                                         |
| ---------------------------- | ------------------------------------------------ |
| 通用for循环                  | 遍历容器（字典是遍历key）                        |
| max()                        | 容器内最大元素                                   |
| min()                        | 容器内最小元素                                   |
| len()                        | 容器元素个数                                     |
| list()                       | 转换为列表                                       |
| tuple()                      | 转换为元组                                       |
| str()                        | 转换为字符串                                     |
| set()                        | 转换为集合                                       |
| sorted(序列, [reverse=True]) | 排序，reverse=True表示降序  得到一个排好序的列表 |

## 9.字符串比较原则

从头到尾一位位进行比较，其中一位大，后面就无需比较了

# 六.python文件操作

## 1.文件的编码

编码就是一种规则集合，记录了内容和二进制间相互转换的逻辑，编码有许多种，我们最常用的是UTF-8编码

![image-20240815094826163](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240815094826163.png)







![image-20240815094829675](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240815094829675.png)

## 2.文件的读取

文件的操作大致可分为三个步骤：打开文件、读写文件、关闭文件，具体操作如下：

### **1.打开文件：**

1.1 基础语法：

```python
文件对象(一般用f代表) = open("文件位置","访问模式",encoding="UTF-8")
```

1.2 三种基础的访问模式：

| **模式** | **描述**                                                     |
| -------- | ------------------------------------------------------------ |
| r        | 以只读方式打开文件。文件的指针将会放在文件的开头。这是默认模式。 |
| w        | 打开一个文件只用于写入。如果该文件已==存在==则打开文件，并==从开头开始编辑==，原有内容会被删除。  如果该文件==不存在==，==创建新文件==。 |
| a        | 打开一个文件用于追加。如果该文件已==存在==，==新的内容将会被写入到已有内容之后==。  如果该文件==不存在==，==创建新文件==进行写入。 |

1.3 案例：

```python
# 1.打开文件，并输出此时的文件类型
f = open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8")
print(f"此时的文件类型为：{type(f)}")
```

![40e99edad392c4eccd53abdfe0f6d111](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/40e99edad392c4eccd53abdfe0f6d111.png)

注意：encoding的顺序在默认函数中不是第三位，所以不能用位置参数，用关键字参数直接指定

----

### **2.读取文件read()：**

2.1 基础语法：

```python
文件对象.read(num)
```

num表示要从文件中读取的数据的长度(单位是字节)，如果没有传入num，那么就表示读取文件中所有的数据

2.2 示例：

```python
# 1.打开文件，并输出此时的文件类型
f = open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8")
print(f"此时的文件类型为：{type(f)}")
# 2.读取文件并输出
print(f"读取文件中的前十个字节：{f.read(10)}")
print(f"读取文件中后面的所有字节：{f.read()}")
```

![bfdca253a4d72cfd7dc2eb721594e5d6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/bfdca253a4d72cfd7dc2eb721594e5d6.png)

2.3 注意：read读取后再使用read读取，那么此时读取的内容会从==上一个==read读取内容的==末尾开始==，并不会从文档的起始部位开始

----

### **3.一次读取一行内容readline()：**

3.1 基础语法：

```python
文件对象.readline()
```

3.2 示例：

```python
# 1.打开文件，并输出此时的文件类型
f = open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8")
print(f"此时的文件类型为：{type(f)}")
# 2.按行读取文件
print(f"第一行为：{f.readline()}")
print(f"第二行为：{f.readline()}")
```

![32617203d6bc1b3e2f39cf894e5bf1a3](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/32617203d6bc1b3e2f39cf894e5bf1a3.png)

3.3 注意：readline()与read()相似，读取一行后指针会自动移动到下一行

----

### **4.读出全部行，并得到列表readlines()：**

4.1 基础语法：

```python
文件对象.readlines()
```

4.2 示例：

```python
# 1.打开文件，并输出此时的文件类型
f = open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8")
print(f"此时的文件类型为：{type(f)}")
# 4.读取文件并返回一个列表：
print(f"读取文件并返回列表输出：{f.readlines()}")
```

![adfda91df33d8ed4dcaf12376305bcd7](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/adfda91df33d8ed4dcaf12376305bcd7.png)

----

### **5.使用for循环得到每一行数据：**

5.1 基础语法：

```python
for line in 文件对象
```

5.2 示例：

```python
# 5.通过for循环读取文件行
for line in open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8"):
    print(line)
```

![ff660ee9099ccd80bbcd4f8869f54b2d](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/ff660ee9099ccd80bbcd4f8869f54b2d.png)

----

### **6.关闭文件close()：**

6.1 语法：

```python
文件对象.close()
```

6.2 注意：如果使用open()函数打开文件后没有关闭程序，那么在外面将无法打开或更改这个被打开的文件，如果想打开或修改这个文件，需要用如下所示

----

### 7.打开后自动关闭文件函数with open() as f:

```python
# 1.打开文件，并输出此时的文件类型
with open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8") as f:
    print(f"此时文件类型为：{type(f)}")
```

注意：句子结尾有冒号，执行完语句块内程序后，会自动关闭文件

----

### 8.文件操作汇总：

| 操作                                   | 功能                                     |
| -------------------------------------- | ---------------------------------------- |
| 文件对象  = open(file, mode, encoding) | 打开文件获得文件对象                     |
| 文件对象.read(num)                     | 读取指定长度字节  不指定num读取文件全部  |
| 文件对象.readline()                    | 读取一行                                 |
| 文件对象.readlines()                   | 读取全部行，得到列表                     |
| for line in 文件对象                   | for循环文件行，一次循环得到一行数据      |
| 文件对象.close()                       | 关闭文件对象                             |
| with open() as f                       | 通过with  open语法打开文件，可以自动关闭 |

9.案例：

![37f1c6caa435016069dbf44a06f6d10b](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/37f1c6caa435016069dbf44a06f6d10b.png)

```python
# 1.打开文件，并输出此时的文件类型
with open("D:/计算机自学/python/文件操作测试.txt","r",encoding="UTF-8") as f:
    content = f.read()    # 将文件中的数据以字符串形式全部读入count内
print(f"itheima在文件中出现了{content.count("itheima")}次")
```

![beff9e9a3048e1c28f3e08f607d747c7](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/beff9e9a3048e1c28f3e08f607d747c7.png)



## 3.文件的写入

1.功能：

| 操作                   | 功能     |
| ---------------------- | -------- |
| f.write("hello world") | 文件写入 |
| f.flush()              | 内容刷新 |

注意：

- 直接调用write，内容并未真正写入文件，而是会积攒在程序的内存中，称之为缓冲区


- 当调用flush的时候，内容会真正写入文件


- 这样做是避免频繁的操作硬盘，导致效率下降(攒一堆，一次性写磁盘)


- 如果文件不存在，使用"w"模式，会创建新文件；如果文件存在，使用"w"模式，会将原有内容清空


- close()方法，带有flush()方法的功能


2.示例：

```python
import time
f = open("D:/计算机自学/python/text.txt","w",encoding="UTF-8")
f.write("hello world")
f.flush()
time.sleep(10000)
```

## 4.文件的追加

1.在打开文件的时候只需要把model的类型改为a即可

```python
f = open("D:/计算机自学/python/text.txt","a",encoding="UTF-8")
```

2.在追加模式下文件的写入函数和上面相同

3.如果想完成换行输入的功能，可以使用\n来达成目的



## 5.文件备份案例



![0ed7be52f2821888fe3698fa48288991](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/0ed7be52f2821888fe3698fa48288991.png)



代码：

```python
# 1.使用open和r模式打开文件并读取
fr = open("D:/计算机自学/python/bill.txt","r",encoding="UTF-8")
# 2.使用open和w模式打开另一个文件用于文件写出
fw = open("D:/计算机自学/python/bill.txt.bak","w",encoding="UTF-8")
# 3.使用for循环将数据读入line中
for line in fr:
    # 4.清理换行符
    line = line.strip()
    # 5.通过split函数对逗号进行分隔,如果是测试，则退出这轮写入循环
    if line.split(",")[4] == "测试":
        continue
    # 6.将内容写出去
    fw.write(line)
    # 7.收到写出换行符
    fw.write("\n")
# 8.关闭文件
fr.close()
fw.close()
```

原文件：

![fc5e3fb165a082d99b16f130077f33fc](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/fc5e3fb165a082d99b16f130077f33fc.png)

新文件：

![87d4037c5a27ad8da87eb4da512046a7](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/87d4037c5a27ad8da87eb4da512046a7.png)

# 七.python异常模块与包

## 1.python异常

1.异常叫bug的来源：来自于计算机中的第一个错误是由于一只小虫子引起的

## 2.异常处理(捕获异常)

1.捕获异常的基本语法：

```python
try:
    可能发生错误的代码
except:
    如果出现异常执行的代码
```

2.捕获指定异常：

```python
try:
    print("name")
except NameError as e:
	print("name变量名称未定义错误")
```

![image-20240816083132472](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816083132472.png)

3.捕获多个异常：

```python
try:
    print(1/0)
except (NameError,ZeroDivisionError) as e:
	print("name变量名称未定义错误")
```

![b2661f63225d2ef604aec3cd2f9f8659](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/b2661f63225d2ef604aec3cd2f9f8659.png)

4.捕获异常并输出描述信息

```python
try:
    print(num)
except (NameError,ZeroDivisionError) as e:
	print(e)
```

![67a560e4578bd2fed3e4c3f3dc57ad00](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/67a560e4578bd2fed3e4c3f3dc57ad00.png)

5.捕获所有异常：

```python
try:
    print(num)
except Exception as e:
	print(e)
```

![67a560e4578bd2fed3e4c3f3dc57ad00](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/67a560e4578bd2fed3e4c3f3dc57ad00.png)

6.异常else：

else表示的是如果没有异常要执行的代码：

```python
try:
    print(1)
except Exception as e:
	print(e)
else:
    print("我是else，是没有异常的时候执行的代码")
```

![215abcc676ae44bb847fe02250aab65b](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/215abcc676ae44bb847fe02250aab65b.png)

7.异常的finally：

finally表示的是无论是否异常都要执行的代码，例如关闭文件：

```python
try:
    f = open("test.txt","r")
except Exception as e:
    f = open("test.txt","w")
else:
    print("没有异常，很开心")
finally：
	f.close()
```

## 3.异常的传递

1.异常具有传递性

![image-20240816093155735](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816093155735.png)



2.上述代码输出语句和结果为：

```python
def func01():
    print("这是func01的开始")
    num = 1 / 0
    print("这是func01的结束")

def func02():
    print("这是func02的开始")
    func01()
    print("这是func02的结束")

def main():
    try:
        func02()
    except Exception as e:
        print(e)

main()
```

![d6b55d049cea9dd1cd183bdbb6db6128](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/d6b55d049cea9dd1cd183bdbb6db6128.png)

## 4.模块的导入

Python模块(Module)，是一个Python文件，以.py结尾，模块能定义函数、类和变量

1.import模块名

**基本语法**：

```python
import 模块名
import 模块名1，模块名2

模块名.功能名()
```

代码案例：

```python
import time
print("你好")
time.sleep(5)
print("我好")
```

2.from 模块名 import 功能名

**基本语法**：

```python
from 模块名 import 功能名
功能名()
```

代码案例：

```python
from time import sleep
print("你好")
sleep(5)
print("我好")
```

3.from 模块名 import *

**基本语法**：

```python
from 模块名 import *
功能名()
```

代码案例：

```python
from time import *
print("你好")
sleep(5)
print("我好")
```

4.as定义别名

**基本语法**：

```python
# 模块定义别名
import 模块名 as 别名
# 功能定义别名
form 模块名 import 功能 as 别名
```

代码案例1：

```python
# 模块别名
import time as tt
print("你好")
tt.sleep(5)
print("我好")
```

代码案例2：

```python
# 功能别名
from time import sleep as sl
print("你好")
sl(5)
print("我好")
```



5.注意事项：

- from可以省略，直接import即可


- as别名可以省略


- 通过点.来确定层级关系


- 模块的导入一般写在代码文件的开头位置


## 5.自定义模块

1.每个python文件都可以作为一个模块，模块的名字就是文件的名字，也就是说自定义模块名必须要符合标识符命名规则

![99caee99681381ed05178f78fa4e4f10](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/99caee99681381ed05178f78fa4e4f10.png)

在调用自定义库时，和调用其他库的方法一致

2.如果在自定义模块时想在模块内加入==测试函数==，并且==不想让函数在主函数内起作用==，可以用如下关键字：

```python
if __name__ == '__main__':
```

这样定义后在主函数内就不会调用测试语句

```python
def test(a,b):
    print(a+b)

# 测试语句，在模块内运行程序时会起作用
if __name__ == '__main__':
    test(1,2)
```

3.注意事项：

当导入多个模块时，且模块内有同名功能，当调用这个同名功能的时候，调用到的是==后面导入的模块的功能==

![image-20240816131735489](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816131735489.png)

4.如果一个模块文件中有`__all__`变量，当使用`from xxx import *`导入时，只能导入这个列表中的元素

![image-20240816132447047](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816132447047.png)

![image-20240816132451390](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816132451390.png)

通过使用all变量可以控制import*的时候哪些功能可以被导入

## 6.自定义包

从物理上看，包就是一个文件夹，在该文件夹下包含了一个__ init __ .py文件

1.定义包步骤如下:

![e96026b8a5f8366a1a9cfb1b37b575f6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e96026b8a5f8366a1a9cfb1b37b575f6.png)

2.导入包

方法一：

```python
import 包名.模块名
包名.模块名.目标
```

![49d82a9a4b69f46170f8b02c5eebe9d8](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/49d82a9a4b69f46170f8b02c5eebe9d8.png)

代码如下：

```python
import my_package.my_module1
import my_package.my_module2
my_package.my_module1.info_print1()
my_package.my_module2.info_print2()
```

方法二：

在__ init __.py文件中添加 all,可以控制导入的模块列表

![image-20240816152442227](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816152442227.png)



![image-20240816152446965](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816152446965.png)

all针对的是from... import ...这种方式，对import xxx这种方式无效



## 7.安装第三方包

1.用cmd安装第三方包：

![image-20240816154224026](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816154224026.png)

如果网速过慢，可以选用清华镜像来完成：

![image-20240816154247074](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816154247074.png)

2.用PyCharm安装第三方包：

![image-20240816154353282](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816154353282.png)



![image-20240816154357226](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816154357226.png)



![image-20240816154400635](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240816154400635.png)



## 8.python的综合案例：

![633b0b4cc642e947d71c7608c8e46799](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/633b0b4cc642e947d71c7608c8e46799.png)

字符串模块：

```python
def str_reverse(s):
    """
    # 1.函数str_reverse(s),接受传入字符串，将字符串反转返回
    :return: 返回反转后的字符串
    """
    return s[::-1]
# 2.函数substr(s,x,y),按照下标x和y，对字符串s进行切片
def substr(s,x,y):
    """
    # 2.函数substr(s,x,y),按照下标x和y，对字符串s进行切片
    :param s:被切片的字符串
    :param x:切片的开始下标
    :param y:切片的结束下标
    :return:切片完成后的字符串
    """
    return s[x:y]

# 测试语句
if __name__ == '__main__':
    print(str_reverse("abcde"))
    print(substr("abcde",1,3))
```

文件处理模块：

```python
def print_file_info(file_name):
    """
    函数1：
    1.函数print_file_info(file_name)接受传入文件的路径，打印文件的全部内容
    2.如果文件不存在则捕获异常,输出提示信息，通过finally关闭文件对象
    """
    # 1.用只读的方式打开文件
    f = open(file_name,"r",encoding="UTF-8")
    # 2.输出文件的全部内容
    print(f.read())
    # 3.关闭文件
    f.close()
def append_to_file(file_name,data):
    """
    函数2：
    1.函数append_to_file(file_name,data)接受文件路径以及传入数据
    2.将数据追加写入到文件中
    """
    # 1.以追加方式打开文件
    f = open(file_name,"a",encoding="UTF-8")
    # 2.将data数据写入文件
    f.write(data)
    # 3.关闭文件
    f.close()

# 测试函数
if __name__ == '__main__':
    append_to_file("D:/计算机自学/python/bill.txt","hello world")
    print_file_info("D:/计算机自学/python/bill.txt")

```

主程序：

```python
import my_utils.str_util
import my_utils.file_util

print(my_utils.str_util.str_reverse("abcde"))
print(my_utils.str_util.substr("abcde",1,3))
```

![1b14576c79adf0c8cb800362be1fcc43](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1b14576c79adf0c8cb800362be1fcc43.png)



# 八.数据可视化——折线图

## 1.JSON数据格式

1.JSON是一种轻量级的数据交互模式，可以按照JSON指定的模式去组织和封装数据；JSON本质上是一个==带有特定格式的字符串==

2.JSON的数据格式有如下两种：

- 括号内的是python中的==字典格式==


```json
{"name":admin,"age":18}
```

- 由字典组成的==列表==：


```json
[{"name":"admin","age":18},{"name":"root","age":16},{"name":"张三","age":20}]
```

3.python数据和json数据的相互转换：

```python
"""
演示json数据和python字典的相互转换
"""
# 导入json包
import json

# 一.用python中的列表转换为json，使用函数：json.dumps(列表,"如果有中文再加上ensure_ascii = False")
# 1.准备列表，列表内的每一个元素都是一个字典
data = [{"name":"张大山","age":11},{"name":"王大锤","age":13},{"name":"赵啸虎","age":16}]
# 2.将python数据转换为json数据：
json_str1 = json.dumps(data,ensure_ascii = False)
print(type(json_str1))
print(json_str1)

# 二.用python中的字典转换为json，使用函数：json.dumps(字典,"如果有中文再加上ensure_ascii = False")
# 1.准备字典
d = {"name":"周锦伦","addr":"台北"}
# 2.将字典转换为json数据
json_str2 = json.dumps(d,ensure_ascii = False)
print(type(json_str2))
print(json_str2)

# 三.将json数据转换为python列表,使用函数：json.loads(json数据)
# 1.定义json数据
s = '[{"name":"张大山","age":11},{"name":"王大锤","age":13},{"name":"赵啸虎","age":16}]'
# 2.将json数据转为列表：
l = json.loads(s)
print(type(l))
print(l)
```

![38adffa29be3029f00869ddf6e2937f0](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/38adffa29be3029f00869ddf6e2937f0.png)

总结：JSON无非就是一个单独的字典或一个内部元素都是字典的列表



## 2.pyecharts模块

1.如果想要做出数据可视化效果图，可以借助pyecharts模块来完成，可通过pip或pycharms来安装其功能包，官方的画廊网站时：https://gallery.pyecharts.org/#/README，官方网站为：pyecharts.org

2.pyecharts的使用：

```python
"""
pyecharts的基础入门
"""
# 调包：
from pyecharts.charts import Line
from pyecharts.options import TitleOpts,LegendOpts,ToolboxOpts,VisualMapOpts
# 1.创建一个折线图对象
line = Line()
# 2.给折线图对象添加x轴数据
line.add_xaxis(["中国","美国","英国"])
# 3.给折线图对象添加y轴数据
line.add_yaxis("GDP",[30,20,10])
# 4.调用render方法，将代码生成为图像
line.render()
```

生成一个html文件，在浏览器中打开如下所示：

![image-20240818195109108](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240818195109108.png)

完善pyechars的功能：

```python
"""
pyecharts的基础入门
"""
# 调包：
from pyecharts.charts import Line
from pyecharts.options import TitleOpts,LegendOpts,ToolboxOpts,VisualMapOpts
# 1.创建一个折线图对象
line = Line()
# 2.给折线图对象添加x轴数据
line.add_xaxis(["中国","美国","英国"])
# 3.给折线图对象添加y轴数据
line.add_yaxis("GDP",[30,20,10])
# 4.设置全局配置项set_global_opts来设置
line.set_global_opts(
    # 令GDP展示标题显示在图标下方正中间
    title_opts=TitleOpts(title="GDP展示",pos_left="center",pos_bottom="1%"),
    legend_opts=LegendOpts(is_show=True),
    # 使用工具箱
    toolbox_opts=ToolboxOpts(is_show=True),
    visualmap_opts=VisualMapOpts(is_show=True),
)
# 5.调用render方法，将代码生成为图像
line.render()
```

![856ad44ab202a35bc769a9baf0093d10](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/856ad44ab202a35bc769a9baf0093d10.png)

pyecharts模块中有许多的配置选项，常用到三个类别的选项：全局配置选项、系列配置选项

全局配置选项可以做诸如以下事情：配置图表的标题、配置图例、配置鼠标移动效果、配置工具栏和等整体配置项



再看就看103课

# 十一.面向对象

## 1.类的定义和方法

1.类的使用语法：

```python
class 类名称:
    # 类的属性，即定义在类中的变量(成员变量)
    类的属性
    # 类的行为，即定义在类中的函数(成员方法)
    类的行为
```

2.创建类对象的语法：

```python
对象 = 类名称()
```

3.成员方法定义时需要使用==self关键字==:

self关键字是成员方法定义的时候，必须填写的

- 它用来表示类对象自身的意思
- 当我们使用类对象调用方法时，self会自动被python传入
- ==在方法内部，想要访问类的成员变量，必须使用self==

```python
def 方法名(self,形参1,...,形参N):
	方法体
    # 在方法内部，想要访问类的成员变量，必须使用self
    print(f"Hi大家好,我是{self.name}")
```

具体示例：

```python
class Student:
    name = None

    def say_hi1(self):
        print(f"大家好，我是{self.name}")

    def say_hi2(self,msg):
        print(f"大家好，我是{self.name},{msg}")


stu = Student()
stu.name = "张三"
stu.say_hi1()
stu.say_hi2("欢迎大家的到来")
```

![4d7470f3382f34c694d77ae62fae8cdc](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4d7470f3382f34c694d77ae62fae8cdc.png)



## 2.构造方法

1.python类可以使用:init()方法，称之为构造方法，构造方法在创建(构造)类的时候，会自动执行；在创建类对象(构造类)的时候，将传入参数自动传递给Init方法使用

```python
__init__()
```

2.构造方法名称前后都有==两个下划线==；在列表中也要提供==self关键字==

```python
class Student:
    name = None
    age = None
    tel = None

    def __init__(self,name,age,tel):
        self.name = name
        self.age = age
        self.tel = tel
        print("Student类创建了一个对象")

stu = Student("周杰伦",18,"31110233")
```

![11aac92cbe296b4d235b358d61298b87](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/11aac92cbe296b4d235b358d61298b87.png)

在python中，__ init __ 不支持方法重载，但是可以通过默认参数、*argc和 ** kwargs或类方法来实现类似的功能

```python
# 默认值重载
class MyClass:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

# 示例
obj1 = MyClass()         # 默认构造
obj2 = MyClass(5)        # 提供一个参数
obj3 = MyClass(5, 10)    # 提供两个参数

print(obj1.x, obj1.y)  # 输出: 0 0
print(obj2.x, obj2.y)  # 输出: 5 0
print(obj3.x, obj3.y)  # 输出: 5 10
```



```python
# 使用*argc 和 **kwargs
class MyClass:
    def __init__(self, *args, **kwargs):
        if len(args) == 1:
            self.data = args[0]
        elif len(args) == 2:
            self.data = args[0] + args[1]
        else:
            self.data = kwargs.get('default', 0)

# 示例
obj1 = MyClass(5)               # 一个参数
obj2 = MyClass(5, 10)           # 两个参数
obj3 = MyClass(default=100)     # 使用关键字参数

print(obj1.data)  # 输出: 5
print(obj2.data)  # 输出: 15
print(obj3.data)  # 输出: 100
```



```python
# 类方法重载：
class MyClass:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    @classmethod
    def from_single_value(cls, value):
        return cls(value, 0)

    @classmethod
    def from_sum(cls, a, b):
        return cls(a + b, a - b)

# 示例
obj1 = MyClass(5, 10)               # 普通构造
obj2 = MyClass.from_single_value(5) # 使用类方法
obj3 = MyClass.from_sum(10, 5)      # 使用类方法

print(obj1.x, obj1.y)  # 输出: 5 10
print(obj2.x, obj2.y)  # 输出: 5 0
print(obj3.x, obj3.y)  # 输出: 15 5
```



## 3.魔术方法

类中使用两个下划线_中间的方法，都被称之为魔术方法

**1.str字符串方法**：

在使用str前输出类时，系统只会输出内存地址：

![image-20240819105515480](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819105515480.png)

使用str方法后：

```python
class Student:
    name = None     # 姓名
    age = None      # 年龄

    def __init__(self,name,age):
        self.name = name
        self.age = age

    def __str__(self):
        return f"Student类的名字是：{self.name},年龄是：{self.age}"

stu1 = Student("周杰伦",11)
print(stu1)
print(str(stu1))
```

![3b7978c058e6a8c7d99b91833c94fca4](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3b7978c058e6a8c7d99b91833c94fca4.png)

**2.lr小于符号比较方法：**

```python
class Student:
    name = None     # 姓名
    age = None      # 年龄

    def __init__(self,name,age):
        self.name = name
        self.age = age

    def __lt__(self,other):
        return self.age < other.age

stu1 = Student("周杰伦",11)
stu2 = Student("林俊杰",22)

print(stu1 < stu2)
```

![4d1fe724a9d62d0da41cb01370ae0727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4d1fe724a9d62d0da41cb01370ae0727.png)



**3.le小于等于符号比较方法：**

```python
class Student:
    name = None     # 姓名
    age = None      # 年龄

    def __init__(self,name,age):
        self.name = name
        self.age = age

    def __le__(self,other):
        return self.age <= other.age

stu1 = Student("周杰伦",11)
stu2 = Student("林俊杰",22)

print(stu1 <= stu2)
```

![4d1fe724a9d62d0da41cb01370ae0727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4d1fe724a9d62d0da41cb01370ae0727.png)



**4.eq相等运算符号实现方法：**



```python
class Student:
    name = None     # 姓名
    age = None      # 年龄

    def __init__(self,name,age):
        self.name = name
        self.age = age

    def __eq__(self, other):
        return self.age == other.age

stu1 = Student("周杰伦",11)
stu2 = Student("林俊杰",11)

print(stu1 == stu2)
```

![4d1fe724a9d62d0da41cb01370ae0727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4d1fe724a9d62d0da41cb01370ae0727.png)



| 方法     | 功能                                           |
| -------- | ---------------------------------------------- |
| __init__ | 构造方法，可用于创建类对象的时候设置初始化行为 |
| __str__  | 用于实现类对象转字符串的行为                   |
| __lt__   | 用于2个类对象进行小于或大于比较                |
| __le__   | 用于2个类对象进行小于等于或大于等于比较        |
| __eq__   | 用于2个类对象进行相等比较                      |



**魔术方法只有这几个吗？**

## 4.私有成员

类中提供了私有成员的形式：

私有成员**变量**：变量名以==两个下划线开头==

私有成员**方法**：方法名以==两个下划线开头==

私有成员无法直接被类对象使用，只能在类内访问

![f9ee746c1aacc5dad909d6188b207b74](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f9ee746c1aacc5dad909d6188b207b74.png)

```python
class Phone:
    __is_5g_enable = False

    def __check_5g(self):
        if self.__is_5g_enable:
            print("5g开启")
        else:
            print("5g关闭，使用4g网络")

    def call_by_5g(self):
        self.__check_5g()
        print("正在通话中")

p = Phone()
p.call_by_5g()
```



![16366e7a0f5bb89ca5849e1ee4ce3124](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/16366e7a0f5bb89ca5849e1ee4ce3124.png)

## 5.继承

**1.继承语法：**

```python
class 类(父类1,父类2,...,父类n):
	类内容体
    pass 		# pass是个占位语句，用来表示函数或类定义的完整性，表示无内容，空的意思
```

**2.多继承中，如果父类有同名方法或属性，==先继承==的==优先级高==于后继承,默认以继承顺序(从左到右)为优先级**

```python
# 1.演示单继承
class Phone:
    IMEI = None     # 序列号
    producer = "ITCAST" # 厂商

    def call_by_4g(self):
        print("4g通话")

class Phone2022(Phone):
    face_id = "10001"       # 面部识别ID

    def call_by_5g(self):
        print("2022年新功能：5g通话")

phone = Phone2022()
print(phone.producer)
phone.call_by_4g()
phone.call_by_5g()
# 2.演示多继承
class NFCReader:
    nfc_type = "第五代"
    producer = "HM"

    def read_card(self):
        print("NFC读卡")

    def write_card(self):
        print("NFC写卡")

class RemoteControl:
    rc_type = "红外遥控"

    def control(self):
        print("红外遥控开启了")

class MyPhone(Phone, NFCReader, RemoteControl):
    pass

phone = MyPhone()
phone.call_by_4g()
phone.read_card()
phone.write_card()
phone.control()

print(phone.producer)
```

![3a74f14b4bda88ed3175acfc6a8bee9b](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3a74f14b4bda88ed3175acfc6a8bee9b.png)



**3.复写和使用父类成员：**

3.1 子类继承父类的成员属性和成员方法后，如果对其"不满意"，那么可以进行复写，即在子类中重新定义同名的属性或方法即可

```python
class Phone:
    IMEI = None             # 序列号
    producer = "ITCAST"     #厂商

    def call_by_5g(self):
        print("父类的5g通话")

class MyPhone(Phone):
    producer = "ITHEIMA"

    def call_by_5g(self):
        print("子类的5g通话")

p = MyPhone()
print(p.producer)
p.call_by_5g()
```

![e1415626e0e2a3c7e89b4746184beb57](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e1415626e0e2a3c7e89b4746184beb57.png)

**3.2 如果需要使用被复写的父类的成员，需要特殊的调用方式：**

方式1：调用父类成员(有self)

```
使用成员变量:父类名.成员变量
使用成员方法:父类名.成员方法(self)
```

方法2：使用super()调用父类成员

```
使用成员变量:super().成员变量
使用成员方法:super().成员方法()
```

示例：

```python
class Phone:
    IMEI = None             # 序列号
    producer = "ITCAST"     #厂商

    def call_by_5g(self):
        print("父类的5g通话")

class MyPhone(Phone):
    producer = "ITHEIMA"
    def call_by_5g(self):
        print(f"方法1调用父类成员producer:{Phone.producer}")
        print(f"方法2调用父类成员producer:{super().producer}")
        # 方法1调用父类成员函数
        Phone.call_by_5g(self)
        # 方法2调用父类成员函数
        super().call_by_5g()
        
p = MyPhone()
p.call_by_5g()
```



![998360b4aedc7b2242131280a8bae799](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/998360b4aedc7b2242131280a8bae799.png)



## 6.变量的类型注解

**1.为变量设置类型注解，基础语法：**

```python
变量:类型
```

![image-20240819145806425](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819145806425.png)



![image-20240819145810907](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819145810907.png)



![image-20240819145831010](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819145831010.png)



![image-20240819145835388](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819145835388.png)



**2.使用type进行注解**

```python
# type:类型
```

![image-20240819150050006](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240819150050006.png)

3.注解仅仅是提示性的，不是决定性的，即使内容与提示不符，也不会报错



## 7.函数和方法的类型注解

1.函数和方法的形参类型注解语法：

```python
def 函数方法名(形参名:类型,形参名:类型...):
    pass
```

示例：

```python
def func(x:int,y:float):
    pass

f = func()
```





![c6582e7e8c005c49e3d4749deac57d88](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/c6582e7e8c005c49e3d4749deac57d88.png)





2.函数和方法的返回值注解语法：

```python
def 函数名方法(形参名:类型,...,形参名:类型) -> 返回值类型:
	pass
```

示例：

```python
def func(x:int,y:float) -> float :
    return x + y

f = func(1,2.0)
```



综上所述：具体语法如下所示

![2afd5b3c30330f195e781ae120cbaace](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/2afd5b3c30330f195e781ae120cbaace.png)



## 8.Union类型注释

1.当类型标注时，要标注的变量有多种类型，此时使用普通的类型标注较为困难，所以可以使用Union进行类型标注

Union类型标注在变量、函数形参和返回值注解中，都可以使用。

```python
# 1.使用Union之前要先调包
from typing import Union

# 2.对列表中的元素进行注解：
my_list: list[Union[int,str]] = [1,2,"itcast","itheima"]
my_dict:dict[str,Union[str,int]] = {"name":"周杰伦","age":13}

# 3.对函数进行类型注解
def func(data : Union[int , str]) -> Union[int,str]:
    pass

func(1)
```



使用之前要先调用typing中的Union功能包，且使用时Union后接的是==中括号==



## 9.多态

1.多态指的是：多种状态，即完成某个行为时，使用不同的对象会得到不同的状态

![89fa8044f3006f3888699ab66cf082db](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/89fa8044f3006f3888699ab66cf082db.png)

2.抽象类：含有抽象方法的类称之为抽象类

抽象方法：方法体是空实现的(pass)称之为抽象方法

示例：

```python
# 1.定义抽象类
class AC:
    # 2.定义抽象方法：
    def cool_wind(self):
        """制冷"""
        pass
    def hot_wind(self):
        """制热"""
        pass
    def swing_l_r(self):
        """左右摆风"""
        pass

# 3.继承抽象类，并重新定义美的方法
class Midea_AC(AC):
    # 定义具体方法：
    def cool_wind(self):
        """制冷"""
        print("美的空调制冷")
    def hot_wind(self):
        """制热"""
        print("美的空调制热")
    def swing_l_r(self):
        """左右摆风"""
        print("美的空调左右吹风")
# 4.继承抽象类，并重新定义格力方法
class GREE_AC(AC):
    # 定义具体方法：
    def cool_wind(self):
        """制冷"""
        print("格力空调制冷")
    def hot_wind(self):
        """制热"""
        print("格力空调制热")
    def swing_l_r(self):
        """左右摆风"""
        print("格力空调左右吹风")

# 5.定义制冷函数，定义传入父类，但是可以传入子类
def make_cool(ac:AC):
    ac.cool_wind()

midea_ac = Midea_AC()
gree_ac = GREE_AC()

# 6.传入不同子类，会有不同输出
make_cool(midea_ac)
make_cool(gree_ac)
```



![f7149944b1a8cefa3146dc24ffa34c87](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f7149944b1a8cefa3146dc24ffa34c87.png)























