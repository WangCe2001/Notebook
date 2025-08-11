# [Kaggle竞赛常用快捷键]()

**取消注释**：ctrl+/

**添加块**：上块a，下块b



# 一.Intro to Programming

## 1. Arithmetic and Variables

导入Titanic竞赛竞赛数据，语句如下：

```python
# Load the data from the titanic competition
import pandas as pd
titanic_data = pd.read_csv("../input/titanic/train.csv")

# Show the first five rows of the data
titanic_data.head()
```

前五行数据如下所示：

![image-20250416091047396](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250416091047396.png)

查看数据的相关信息：

```python
# Number of total passengers
total = len(titanic_data)
print(total)

# Number of passengers who survived
survived = (titanic_data.Survived == 1).sum()
print(survived)

# Number of passengers under 18
minors = (titanic_data.Age < 18).sum()
print(minors)

# 输出结果如下：
>>>891 有891人在泰坦尼克号的船上
>>>342 有342名乘客活下来了
>>>113 有113名乘客年龄小于18岁
```



## 2. Functions

这章是关于函数的一些定义与操作，没什么问题



## 3.Data Types

这章介绍了一些数据类型，比如整数、小数、布尔值和字符串

强制类型转换：小数向0值方向靠近

```python
# Uncomment and run this code to get started!
print(int(1.2321))
print(int(1.747))
print(int(-3.94535))
print(int(-2.19774))

>>>1
>>>1
>>>-3
>>>-2
```



## 4.Conditions and Conditional Statements

这章主要介绍了一些条件语句

可以使用if...elif...else这种语句：

```python
def evaluate_temp_with_elif(temp):
    if temp > 38:
        message = "Fever!"
    elif temp > 35:
        message = "Normal temperature."
    else:
        message = "Low temperature."
    return message
```



## 5.Intro to Lists

这章主要介绍了一些列表的操作：

**定义列表：**

```python
flowers_list = ["pink primrose", "hard-leaved pocket orchid", "canterbury bells", "sweet pea", "english marigold", "tiger lily", "moon orchid", "bird of paradise", "monkshood", "globe thistle"]

print(type(flowers_list))
print(flowers_list)

# 输出结果为：
<class 'list'>
['pink primrose', 'hard-leaved pocket orchid', 'canterbury bells', 'sweet pea', 'english marigold', 'tiger lily', 'moon orchid', 'bird of paradise', 'monkshood', 'globe thistle']
```

**长度：**

```python
# The list has ten entries
print(len(flowers_list))
>>> 10
```

**索引：**

```python
print("First entry:", flowers_list[0])
print("Second entry:", flowers_list[1])

# The list has length ten, so we refer to final entry with 9
print("Last entry:", flowers_list[9])

>>>First entry: pink primrose
>>>Second entry: hard-leaved pocket orchid
>>>Last entry: globe thistle
```

**切片：**

```python
print("First three entries:", flowers_list[:3])
print("Final two entries:", flowers_list[-2:])

>>>First three entries: ['pink primrose', 'hard-leaved pocket orchid', 'canterbury bells']
>>>Final two entries: ['monkshood', 'globe thistle']
```

**删除：**

```python
flowers_list.remove("globe thistle")
print(flowers_list)

>>>['pink primrose', 'hard-leaved pocket orchid', 'canterbury bells', 'sweet pea', 'english marigold', 'tiger lily', 'moon orchid', 'bird of paradise', 'monkshood']
```

**添加：**

```python
flowers_list.append("snapdragon")
print(flowers_list)

>>>['pink primrose', 'hard-leaved pocket orchid', 'canterbury bells', 'sweet pea', 'english marigold', 'tiger lily', 'moon orchid', 'bird of paradise', 'monkshood', 'snapdragon']
```

**最大、最小、求和：**

```python
# Do not change: Number of customers each day for the last month
num_customers = [137, 147, 135, 128, 170, 174, 165, 146, 126, 159,
                 141, 148, 132, 147, 168, 153, 170, 161, 148, 152,
                 141, 151, 131, 149, 164, 163, 143, 143, 166, 171]

# TODO: Fill in values for the variables below
avg_first_seven = sum(num_customers[:7])/7
avg_last_seven = sum(num_customers[-7:])/7 
max_month = max(num_customers)
min_month = min(num_customers)

# Do not change: Check your answer
q2.check()
```

**字符串转换为列表：**

```python
flowers = "pink primrose,hard-leaved pocket orchid,canterbury bells,sweet pea,english marigold,tiger lily,moon orchid,bird of paradise,monkshood,globe thistle"

print(flowers.split(","))

>>>['pink primrose', 'hard-leaved pocket orchid', 'canterbury bells', 'sweet pea', 'english marigold', 'tiger lily', 'moon orchid', 'bird of paradise', 'monkshood', 'globe thistle']
```

**使用for循环进行测试：**

```python
test_liked = [i>=4 for i in test_ratings]
print(test_liked)

>>>[False, False, False, True, True]
```



# 二.Python

## 1.Hello，Python

这章介绍了python的一些基础语法

**除法：**

```python
print(5 / 2)
print(6 / 2)

>>>2.5
>>>3.0
```

**整除：**

```python
print(5 // 2)
print(6 // 2)

>>>2
>>>3
```

**交换：**

```python
a, b = b, a
```



## 2.Functions and Getting Help

**帮助：**

```python
help(round)

# 输出结果：
Help on built-in function round in module builtins:

round(number, ndigits=None)
    Round a number to a given precision in decimal digits.
    
    The return value is an integer if ndigits is omitted or None.  Otherwise
    the return value has the same type as the number.  ndigits may be negative.
```

**函数注释：**

```python
def least_difference(a, b, c):
    """Return the smallest difference between any two numbers
    among a, b and c.
    
    >>> least_difference(1, 5, -5)
    4
    """
    diff1 = abs(a - b)
    diff2 = abs(b - c)
    diff3 = abs(a - c)
    return min(diff1, diff2, diff3)
```

使用help查看这个函数的解释：

```python
help(least_difference)


Help on function least_difference in module __main__:

least_difference(a, b, c)
    Return the smallest difference between any two numbers
    among a, b and c.
    
    >>> least_difference(1, 5, -5)
    4
```

**更高指令函数：**

```python
def mod_5(x):
    """Return the remainder of x after dividing by 5"""
    return x % 5

print(
    'Which number is biggest?',
    max(100, 51, 14),
    'Which number is the biggest modulo 5?',
    max(100, 51, 14, key=mod_5),
    sep='\n',
)

# 输出如下：
Which number is biggest?
100
Which number is the biggest modulo 5?
14
```

**round函数使用：**

```python
round(3.14159,2)
>>> 3.14

round(1232.345,-2)
>>> 1200
```



## 3.Booleans and Conditionals

这章没啥不懂的

## 4.Lists

具体操控可看python语法



## 5.Loops and List Comprehensions

**循环输出：**

```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
for planet in planets:
    print(planet, end=' ') # print all on same line   
>>> Mercury Venus Earth Mars Jupiter Saturn Uranus Neptune 

squares = [n**2 for n in range(10)]
>>> [0, 1, 4, 9, 16, 25, 36, 49, 64, 81]

short_planets = [planet for planet in planets if len(planet) < 6]
>>> ['Venus', 'Earth', 'Mars']

loud_short_planets = [planet.upper() + '!' for planet in planets if len(planet) < 6]
>>> ['VENUS!', 'EARTH!', 'MARS!']
```



## 6.Strings and Dictionaries

**引号中有引号：**

```python
'Pluto\'s a planet!'
>>> "Pluto's a planet!"
```

字符串的引号运用表格：

| What you type... | What you get | example                   | `print(example)`       |
| :--------------- | :----------- | :------------------------ | :--------------------- |
| `\'`             | `'`          | `'What\'s up?'`           | `What's up?`           |
| `\"`             | `"`          | `"That's \"cool\""`       | `That's "cool"`        |
| `\\`             | `\`          | `"Look, a mountain: /\\"` | `Look, a mountain: /\` |
| `\n`             |              | `"1\n2 3"`                | `1` `2 3`              |

**字符串字符：**

```python
hello = "hello\nworld"
print(hello)
>>> hello
>>> world
```

**字符串方法：**

```python
# ALL CAPS
claim = "Pluto is a planet!"
claim.upper()
>>> 'PLUTO IS A PLANET!'

# all lowercase
claim.lower()
>>> 'pluto is a planet!'

# Searching for the first index of a substring
claim.index('plan')
>>> 11

claim.startswith(planet)
>>> True

# false because of missing exclamation mark
claim.endswith('planet')
>>> False

words = claim.split()
>>> ['Pluto', 'is', 'a', 'planet!']

datestr = '1956-01-31'
year, month, day = datestr.split('-')
'/'.join([month, day, year])
>>> '01/31/1956'

"{}, you'll always be the {}th planet to me.".format(planet, position)
>>> "Pluto, you'll always be the 9th planet to me."

# Referring to format() arguments by index, starting from 0
s = """Pluto's a {0}.
No, it's a {1}.
{0}!
{1}!""".format('planet', 'dwarf planet')
print(s)
>>> Pluto's a planet.
>>> No, it's a dwarf planet.
>>> planet!
>>> dwarf planet!

```

**字典：**

```python
planets = ['Mercury', 'Venus', 'Earth', 'Mars', 'Jupiter', 'Saturn', 'Uranus', 'Neptune']
planet_to_initial = {planet: planet[0] for planet in planets}
planet_to_initial

>>> {'Mercury': 'M',
 'Venus': 'V',
 'Earth': 'E',
 'Mars': 'M',
 'Jupiter': 'J',
 'Saturn': 'S',
 'Uranus': 'U',
 'Neptune': 'N'}

'Saturn' in planet_to_initial
>>> True

'Betelgeuse' in planet_to_initial
>>> False

numbers = {'one': 'Pluto', 'two': 2, 'three': 3, 'eleven': 11}
for k in numbers:
    print("{} = {}".format(k, numbers[k]))
>>> one = Pluto
two = 2
three = 3
eleven = 11
```



## 7.Working with External Libraries

**导包：**

```python
import math
import math as mt
from math import *
from math import log,pi
```





# 三.Intro to Machine Learning



## 1.How Models Work

无，介绍了下决策树



## 2.Basic Data Exploration

无，简单介绍了下数据操作



## 3.Your First Machine Learning Model

**建立模型的步骤：**

- 定义：定义我们要使用的模型类型
- 拟合：从被提供的数据中捕获模式
- 预测：看模型预测的结果
- 评估：定义用什么准则来评估模型的好坏







## 4.Model Validation

**模型验证：**MAE(Mean Absolute Error)平均绝对值错误

**模型使用过程：**

```python
# Import the train_test_split function and uncomment
from sklearn.model_selection import train_test_split

# fill in and uncomment
train_X, val_X, train_y, val_y = train_test_split(X, y, random_state = 1)

# You imported DecisionTreeRegressor in your last exercise
# and that code has been copied to the setup code above. So, no need to
# import it again
from sklearn.tree import DecisionTreeRegressor

# Specify the model
iowa_model = DecisionTreeRegressor(random_state = 1)

# Fit iowa_model with the training data.
iowa_model.fit(train_X, train_y)

# Predict with all validation observations
val_predictions = iowa_model.predict(val_X)

# print the top few validation predictions
print(iowa_model.predict(X.head()))
# print the top few actual prices from validation data
print(val_y)

from sklearn.metrics import mean_absolute_error
val_mae = mean_absolute_error(val_y,val_predictions)

# uncomment following line to see the validation_mae
print(val_mae)
```





## 5.Underfitting and Overfitting

**欠拟合与过拟合图像：**

![underfitting_overfitting](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/AXSEOfI.png)

## 6.Random Forests

**随机森林模型：**

```python
from sklearn.ensemble import RandomForestRegressor

# Define the model. Set random_state to 1
rf_model = RandomForestRegressor(random_state = 1)

# fit your model
rf_model.fit(train_X, train_y)

# Calculate the mean absolute error of your Random Forest model on the validation data
rf_val_mae = mean_absolute_error(val_y, rf_model.predict(val_X))

print("Validation MAE for Random Forest Model: {}".format(rf_val_mae))
```



## 7.Machine Learning Competitions 

教我们如何提交自己的结果到比赛中的：

![image-20250417102014974](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250417102014974.png)







# 四.Pandns



## 1.Creating,Reading and Writing

有两种数据类型在pandas中，分别为**DataFrame**和**Series**

### 1.1 创建DataFrame：

```python
import pandas as pd
# 创建数据
pd.DataFrame({'Yes': [50, 21], 'No': [131, 2]})
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 'Sue': ['Pretty good.', 'Bland.']})
pd.DataFrame({'Bob': ['I liked it.', 'It was awful.'], 
              'Sue': ['Pretty good.', 'Bland.']},
             index=['Product A', 'Product B'])
fruits = pd.DataFrame([[30,21]],columns=['Apples','Bananas'])
fruit_sales = pd.DataFrame([[35,21],[41,34]],columns=['Apples','Bananas'],index=['2017 Sales','2018 Sales'])

```

数据输出类型：

![image-20250417111248840](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250417111248840.png)

![image-20250417111305796](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250417111305796.png)

![image-20250417111400239](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250417111400239.png)

![image-20250421093628722](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250421093628722.png)

![image-20250421094045984](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250421094045984.png)



### **1.2 创建Series：**

```python
import pandas as pd
pd.Series([1, 2, 3, 4, 5])
pd.Series([30, 35, 40], index=['2015 Sales', '2016 Sales', '2017 Sales'], name='Product A')
```

![image-20250421091242479](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250421091242479.png)

### **1.3 CSV格式**

CSV (Comma-Seperated Values) 格式是用逗号作为间隔符的文件格式：

```csv
Product A,Product B,Product C,
30,21,9,
35,34,1,
41,11,11
```





### **1.4 读取数据：**

```python
wine_reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv")
wine_reviews.shape
>>> （129971，14）
wine_reviews.head()
```

输出效果：

|      | Unnamed: 0 | country  | description                                       | designation                        | points | price | province          | region_1            | region_2          | taster_name        | taster_twitter_handle | title                                             | variety        | winery              |
| :--- | ---------- | -------- | ------------------------------------------------- | ---------------------------------- | ------ | ----- | ----------------- | ------------------- | ----------------- | ------------------ | --------------------- | ------------------------------------------------- | -------------- | ------------------- |
| 0    | 0          | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                       | 87     | NaN   | Sicily & Sardinia | Etna                | NaN               | Kerin O’Keefe      | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia             |
| 1    | 1          | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                           | 87     | 15.0  | Douro             | NaN                 | NaN               | Roger Voss         | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos |
| 2    | 2          | US       | Tart and snappy, the flavors of lime flesh and... | NaN                                | 87     | 14.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Rainstorm 2013 Pinot Gris (Willamette Valley)     | Pinot Gris     | Rainstorm           |
| 3    | 3          | US       | Pineapple rind, lemon pith and orange blossom ... | Reserve Late Harvest               | 87     | 13.0  | Michigan          | Lake Michigan Shore | NaN               | Alexander Peartree | NaN                   | St. Julian 2013 Reserve Late Harvest Riesling ... | Riesling       | St. Julian          |
| 4    | 4          | US       | Much like the regular bottling from 2012, this... | Vintner's Reserve Wild Child Block | 87     | 65.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Sweet Cheeks 2012 Vintner's Reserve Wild Child... | Pinot Noir     | Sweet Cheeks        |



使用第一列作为索引：

```python
wine_reviews = pd.read_csv("../input/wine-reviews/winemag-data-130k-v2.csv", index_col=0)
wine_reviews.head()
```

输出结果：

|      | country  | description                                       | designation                        | points | price | province          | region_1            | region_2          | taster_name        | taster_twitter_handle | title                                             | variety        | winery              |
| :--- | -------- | ------------------------------------------------- | ---------------------------------- | ------ | ----- | ----------------- | ------------------- | ----------------- | ------------------ | --------------------- | ------------------------------------------------- | -------------- | ------------------- |
| 0    | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                       | 87     | NaN   | Sicily & Sardinia | Etna                | NaN               | Kerin O’Keefe      | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia             |
| 1    | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                           | 87     | 15.0  | Douro             | NaN                 | NaN               | Roger Voss         | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos |
| 2    | US       | Tart and snappy, the flavors of lime flesh and... | NaN                                | 87     | 14.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Rainstorm 2013 Pinot Gris (Willamette Valley)     | Pinot Gris     | Rainstorm           |
| 3    | US       | Pineapple rind, lemon pith and orange blossom ... | Reserve Late Harvest               | 87     | 13.0  | Michigan          | Lake Michigan Shore | NaN               | Alexander Peartree | NaN                   | St. Julian 2013 Reserve Late Harvest Riesling ... | Riesling       | St. Julian          |
| 4    | US       | Much like the regular bottling from 2012, this... | Vintner's Reserve Wild Child Block | 87     | 65.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Sweet Cheeks 2012 Vintner's Reserve Wild Child... | Pinot Noir     | Sweet Cheeks        |



### **1.5 将数据保存为CSV格式：**

```python
animals.to_csv("cows_and_goats.csv")
```



## 2.Indexing,Seleccting & Assigning

### **2.1 默认访问：**

首先读入数据如下所示：

```python
reviews
```

显示结果如下：

|      | country  | description                                       | designation                        | points | price | province          | region_1            | region_2          | taster_name        | taster_twitter_handle | title                                             | variety        | winery              |
| :--- | -------- | ------------------------------------------------- | ---------------------------------- | ------ | ----- | ----------------- | ------------------- | ----------------- | ------------------ | --------------------- | ------------------------------------------------- | -------------- | ------------------- |
| 0    | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                       | 87     | NaN   | Sicily & Sardinia | Etna                | NaN               | Kerin O’Keefe      | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia             |
| 1    | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                           | 87     | 15.0  | Douro             | NaN                 | NaN               | Roger Voss         | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos |
| 2    | US       | Tart and snappy, the flavors of lime flesh and... | NaN                                | 87     | 14.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Rainstorm 2013 Pinot Gris (Willamette Valley)     | Pinot Gris     | Rainstorm           |
| 3    | US       | Pineapple rind, lemon pith and orange blossom ... | Reserve Late Harvest               | 87     | 13.0  | Michigan          | Lake Michigan Shore | NaN               | Alexander Peartree | NaN                   | St. Julian 2013 Reserve Late Harvest Riesling ... | Riesling       | St. Julian          |
| 4    | US       | Much like the regular bottling from 2012, this... | Vintner's Reserve Wild Child Block | 87     | 65.0  | Oregon            | Willamette Valley   | Willamette Valley | Paul Gregutt       | @paulgwine            | Sweet Cheeks 2012 Vintner's Reserve Wild Child... | Pinot Noir     | Sweet Cheeks        |

129971 rows x 13 columns

访问数据：

In[3]:

```python
reviews.country
```

Out[3]:

```
0            Italy
1         Portugal
            ...   
129969      France
129970      France
Name: country, Length: 129971, dtype: object
```

In[4]:

```python
reviews['country']
```

Out[4]:

```
0            Italy
1         Portugal
            ...   
129969      France
129970      France
Name: country, Length: 129971, dtype: object
```

In[5]:

```python
reviews['country'][0]
```

Out[5]:

```
'Italy'
```



### **2.2 Pandas中的索引**

有两种基本的使用语法，分别为iloc和loc，二者之间的使用例子可看下方代码，二者之间的不同：

iloc[0:10]，选择的是0,1,...,8,9，一般使用数字索引

loc[0:10]，选择的是0,1,...,8,9,10，一般使用名称索引

#### **2.2.1 Index-based selection:**

In[6]:查看第一行数据

```python
reviews.iloc[0]
```

Out[6]:

```
country                                                    Italy
description    Aromas include tropical fruit, broom, brimston...
                                     ...                        
variety                                              White Blend
winery                                                   Nicosia
Name: 0, Length: 13, dtype: object
```

In [7]:查看第一列数据

```python
reviews.iloc[:, 0]
```

Out[7]:

```
0            Italy
1         Portugal
            ...   
129969      France
129970      France
Name: country, Length: 129971, dtype: object
```

In [8]:查看前三行的第一列数据

```python
reviews.iloc[:3, 0]
```

Out[8]:

```
0       Italy
1    Portugal
2          US
Name: country, dtype: object
```

In [10]:

```
reviews.iloc[[0, 1, 2], 0]
```

Out[10]:查看前三行的第一列数据

```
0       Italy
1    Portugal
2          US
Name: country, dtype: object
```



#### **2.2.2 Label-based selection**

In [12]:查看country列的第一行数据

```python
reviews.loc[0, 'country']
```

Out[12]:

```
'Italy'
```



In [13]:查看三列所有行数据

```python
reviews.loc[:, ['taster_name', 'taster_twitter_handle', 'points']]
```

Out[13]:

|        | taster_name   | taster_twitter_handle | points |
| :----- | :------------ | :-------------------- | :----- |
| 0      | Kerin O’Keefe | @kerinokeefe          | 87     |
| 1      | Roger Voss    | @vossroger            | 87     |
| ...    | ...           | ...                   | ...    |
| 129969 | Roger Voss    | @vossroger            | 90     |
| 129970 | Roger Voss    | @vossroger            | 90     |

129971 rows × 3 columns





### **2.3 改变索引：**

通过上面的例子我们知道，我们可以使用loc来进行数据的索引，为了改变索引参数，我们可以使用以后的一列作为索引值，title是我们已有的一列数据，现设置为新的索引：

In [14]:

```python
reviews.set_index("title")
```

Out[14]:

|                                                              | country  | description                                       | designation                   | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | variety        | winery               |
| :----------------------------------------------------------- | :------- | :------------------------------------------------ | :---------------------------- | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------- | :------------------- |
| title                                                        |          |                                                   |                               |        |       |                   |          |          |               |                       |                |                      |
| Nicosia 2013 Vulkà Bianco (Etna)                             | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | 87     | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | White Blend    | Nicosia              |
| Quinta dos Avidagos 2011 Avidagos Red (Douro)                | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                      | 87     | 15.0  | Douro             | NaN      | NaN      | Roger Voss    | @vossroger            | Portuguese Red | Quinta dos Avidagos  |
| ...                                                          | ...      | ...                                               | ...                           | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...            | ...                  |
| Domaine Marcel Deiss 2012 Pinot Gris (Alsace)                | France   | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90     | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Pinot Gris     | Domaine Marcel Deiss |
| Domaine Schoffit 2012 Lieu-dit Harth Cuvée Caroline Gewurztraminer (Alsace) | France   | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90     | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            |                |                      |



### **2.4 有条件的选择：**

In [15]:

```python
reviews.country == 'Italy'
```

Out[15]:

```
0          True
1         False
          ...  
129969    False
129970    False
Name: country, Length: 129971, dtype: bool
```



In [16]:输出国家是Italy的数据

```python
reviews.loc[reviews.country == 'Italy']
```

Out[16]:

|        | country | description                                       | designation               | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety      | winery          |
| :----- | :------ | :------------------------------------------------ | :------------------------ | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :----------- | :-------------- |
| 0      | Italy   | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco              | 87     | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend  | Nicosia         |
| 6      | Italy   | Here's a bright, informal red that opens with ... | Belsito                   | 87     | 16.0  | Sicily & Sardinia | Vittoria | NaN      | Kerin O’Keefe | @kerinokeefe          | Terre di Giurfo 2013 Belsito Frappato (Vittoria)  | Frappato     | Terre di Giurfo |
| ...    | ...     | ...                                               | ...                       | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...          | ...             |
| 129961 | Italy   | Intense aromas of wild cherry, baking spice, t... | NaN                       | 90     | 30.0  | Sicily & Sardinia | Sicilia  | NaN      | Kerin O’Keefe | @kerinokeefe          | COS 2013 Frappato (Sicilia)                       | Frappato     | COS             |
| 129962 | Italy   | Blackberry, cassis, grilled herb and toasted a... | Sàgana Tenuta San Giacomo | 90     | 40.0  | Sicily & Sardinia | Sicilia  | NaN      | Kerin O’Keefe | @kerinokeefe          | Cusumano 2012 Sàgana Tenuta San Giacomo Nero d... | Nero d'Avola | Cusumano        |

19540 rows × 13 columns

#### **使用&**

In [17]:

```python
reviews.loc[(reviews.country == 'Italy') & (reviews.points >= 90)]
```

Out[17]:

|        | country | description                                       | designation               | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety      | winery   |
| :----- | :------ | :------------------------------------------------ | :------------------------ | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :----------- | :------- |
| 120    | Italy   | Slightly backward, particularly given the vint... | Bricco Rocche Prapó       | 92     | 70.0  | Piedmont          | Barolo   | NaN      | NaN           | NaN                   | Ceretto 2003 Bricco Rocche Prapó (Barolo)         | Nebbiolo     | Ceretto  |
| 130    | Italy   | At the first it was quite muted and subdued, b... | Bricco Rocche Brunate     | 91     | 70.0  | Piedmont          | Barolo   | NaN      | NaN           | NaN                   | Ceretto 2003 Bricco Rocche Brunate (Barolo)       | Nebbiolo     | Ceretto  |
| ...    | ...     | ...                                               | ...                       | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...          | ...      |
| 129961 | Italy   | Intense aromas of wild cherry, baking spice, t... | NaN                       | 90     | 30.0  | Sicily & Sardinia | Sicilia  | NaN      | Kerin O’Keefe | @kerinokeefe          | COS 2013 Frappato (Sicilia)                       | Frappato     | COS      |
| 129962 | Italy   | Blackberry, cassis, grilled herb and toasted a... | Sàgana Tenuta San Giacomo | 90     | 40.0  | Sicily & Sardinia | Sicilia  | NaN      | Kerin O’Keefe | @kerinokeefe          | Cusumano 2012 Sàgana Tenuta San Giacomo Nero d... | Nero d'Avola | Cusumano |

6648 rows × 13 columns

#### **使用|**

In [18]:

```python
reviews.loc[(reviews.country == 'Italy') | (reviews.points >= 90)]
```

Out[18]:

|        | country | description                                       | designation                   | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety        | winery               |
| :----- | :------ | :------------------------------------------------ | :---------------------------- | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| 0      | Italy   | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | 87     | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia              |
| 6      | Italy   | Here's a bright, informal red that opens with ... | Belsito                       | 87     | 16.0  | Sicily & Sardinia | Vittoria | NaN      | Kerin O’Keefe | @kerinokeefe          | Terre di Giurfo 2013 Belsito Frappato (Vittoria)  | Frappato       | Terre di Giurfo      |
| ...    | ...     | ...                                               | ...                           | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...            | ...                  |
| 129969 | France  | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90     | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970 | France  | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90     | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

61937 rows × 13 columns

#### **.isin():挑选符合条件的数据：**

In [19]:

```python
reviews.loc[reviews.country.isin(['Italy', 'France'])]
```

Out[19]:

|        | country | description                                       | designation                   | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety        | winery               |
| :----- | :------ | :------------------------------------------------ | :---------------------------- | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| 0      | Italy   | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | 87     | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia              |
| 6      | Italy   | Here's a bright, informal red that opens with ... | Belsito                       | 87     | 16.0  | Sicily & Sardinia | Vittoria | NaN      | Kerin O’Keefe | @kerinokeefe          | Terre di Giurfo 2013 Belsito Frappato (Vittoria)  | Frappato       | Terre di Giurfo      |
| ...    | ...     | ...                                               | ...                           | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...            | ...                  |
| 129969 | France  | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90     | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970 | France  | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90     | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

41633 rows × 13 columns

#### **.isnull():挑选出不为零的数据：**

In [20]:

```python
reviews.loc[reviews.price.notnull()]
```

Out[20]:

|        | country  | description                                       | designation                   | points | price | province | region_1          | region_2          | taster_name  | taster_twitter_handle | title                                             | variety        | winery               |
| :----- | :------- | :------------------------------------------------ | :---------------------------- | :----- | :---- | :------- | :---------------- | :---------------- | :----------- | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| 1      | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                      | 87     | 15.0  | Douro    | NaN               | NaN               | Roger Voss   | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos  |
| 2      | US       | Tart and snappy, the flavors of lime flesh and... | NaN                           | 87     | 14.0  | Oregon   | Willamette Valley | Willamette Valley | Paul Gregutt | @paulgwine            | Rainstorm 2013 Pinot Gris (Willamette Valley)     | Pinot Gris     | Rainstorm            |
| ...    | ...      | ...                                               | ...                           | ...    | ...   | ...      | ...               | ...               | ...          | ...                   | ...                                               | ...            | ...                  |
| 129969 | France   | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90     | 32.0  | Alsace   | Alsace            | NaN               | Roger Voss   | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970 | France   | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90     | 21.0  | Alsace   | Alsace            | NaN               | Roger Voss   | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

120975 rows × 13 columns

### 2.5 分配数据

In [21]:

```python
reviews['critic'] = 'everyone'
```

Out[21]:

```
0         everyone
1         everyone
            ...   
129969    everyone
129970    everyone
Name: critic, Length: 129971, dtype: object
```



## 3.Summary Functions and Maps

摘要函数和映射

### 3.1 摘要函数

#### **3.1.1 .describe()函数：看一些参数值**

In [3]:

```python
reviews.points.describe()
```

Out[3]:

```
count    129971.000000
mean         88.447138
             ...      
75%          91.000000
max         100.000000
Name: points, Length: 8, dtype: float64
```



#### **3.1.2 .mean()函数：看平均值**

In [5]:

```python
reviews.points.mean()
```

Out[5]:

```
88.44713820775404
```



#### **3.1.3 .unique()函数：将有重复的值唯一输出**

In [6]:

```python
reviews.taster_name.unique()
```

Out[6]:

```
array(['Kerin O’Keefe', 'Roger Voss', 'Paul Gregutt',
       'Alexander Peartree', 'Michael Schachner', 'Anna Lee C. Iijima',
       'Virginie Boone', 'Matt Kettmann', nan, 'Sean P. Sullivan',
       'Jim Gordon', 'Joe Czerwinski', 'Anne Krebiehl\xa0MW',
       'Lauren Buzzeo', 'Mike DeSimone', 'Jeff Jenssen',
       'Susan Kostrzewa', 'Carrie Dykes', 'Fiona Adams',
       'Christina Pickard'], dtype=object)
```



#### **3.1.4 .value_counts()：查看数据在数据集中出现的次数**

In [7]:

```python
reviews.taster_name.value_counts()
```

Out[7]:

```
Roger Voss           25514
Michael Schachner    15134
                     ...  
Fiona Adams             27
Christina Pickard        6
Name: taster_name, Length: 19, dtype: int64
```



### 3.2 数据处理函数map和apply

map和apply函数都不改变原数据，而是生成一个新的数据

#### **3.2.1 map()：**主要对Series(一般是一列数据)中的每一个元素进行映射操作

In [8]:

```python
review_points_mean = reviews.points.mean()
reviews.points.map(lambda p: p - review_points_mean)
```

Out[8]:

```
0        -1.447138
1        -1.447138
            ...   
129969    1.552862
129970    1.552862
Name: points, Length: 129971, dtype: float64
```

==使用字典映射例子：==

```python
import pandas as pd

df = pd.DataFrame({
    'gender': ['M', 'F', 'F', 'M']
})

# 将性别编码为数字
mapping = {'M': 1, 'F': 0}
df['gender_code'] = df['gender'].map(mapping)

print(df)

>>>
     gender  gender_code
0      M            1
1      F            0
2      F            0
3      M            1
```

==使用函数映射：==

```python
# 将每个名字首字母变小写
df['gender_lower'] = df['gender'].map(lambda x: x.lower())
print(df)

>>>
    gender  gender_code gender_lower
0      M            1            m
1      F            0            f
2      F            0            f
3      M            1            m
```



#### **3.2.2 apply()函数：**对DataFrame或Series的每个元素、每一行或每一列应用一个函数

In [9]:

```python
def remean_points(row):
    row.points = row.points - review_points_mean
    return row

reviews.apply(remean_points, axis='columns')
```

Out[9]:

|        | country  | description                                       | designation                   | points    | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety        | winery               |
| :----- | :------- | :------------------------------------------------ | :---------------------------- | :-------- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| 0      | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | -1.447138 | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia              |
| 1      | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                      | -1.447138 | 15.0  | Douro             | NaN      | NaN      | Roger Voss    | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos  |
| ...    | ...      | ...                                               | ...                           | ...       | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...            | ...                  |
| 129969 | France   | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 1.552862  | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970 | France   | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 1.552862  | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

129971 rows × 13 columns

==对DataFrame使用：==

```python
df = pd.DataFrame({
    'A': [1, 2, 3],
    'B': [10, 20, 30]
})

# 对每列求最大值减去最小值
col_range = df.apply(lambda x: x.max() - x.min())
print(col_range)

>>>
A     2
B    20
dtype: int64
```



==通过符号改变数据：==

In [12]:

```python
reviews.country + " - " + reviews.region_1
```

Out[12]:

```
0            Italy - Etna
1                     NaN
               ...       
129969    France - Alsace
129970    France - Alsace
Length: 129971, dtype: object
```



## 4.Grouping and Sorting



### 4.1 分类聚合函数：groupby()

**基本作用：**将数据按某一列或多列分组，对每个分组进行统计、聚合、变换等操作

**基本语法：**

```python
df.groupby('列名')
df.groupby(['列1', '列2'])
```

通常会和聚合函数(如sum()、mean()、count()等)一起使用

```python
df.groupby('列名').聚合函数()
```



**按单列分组统计：**

```python
import pandas as pd

df = pd.DataFrame({
    'class': ['A', 'A', 'B', 'B', 'C'],
    'score': [80, 85, 90, 88, 92]
})

# 按班级分组，求每个班级的平均分
result = df.groupby('class')['score'].mean()
print(result)

>>>
class
A    82.5
B    89.0
C    92.0
Name: score, dtype: float64
```



**按多列分组：**

```python
df2 = pd.DataFrame({
    'gender': ['M', 'F', 'M', 'F', 'M'],
    'class': ['A', 'A', 'B', 'B', 'C'],
    'score': [80, 85, 90, 88, 92]
})

# 按性别和班级分组，求每组的平均分
result2 = df2.groupby(['gender', 'class'])['score'].mean()
print(result2)

>>>
gender  class
F       A        85
        B        88
M       A        80
        B        90
        C        92
Name: score, dtype: int64
```



**分组后应用多个聚合函数：**

```python
# 求每个班级的平均分和总分
result3 = df.groupby('class')['score'].agg(['mean', 'sum'])
print(result3)

>>>
		mean  sum
class            
A       82.5  165
B       89.0  178
C       92.0   92
```





### 4.2 多索引整合

使用groupby函数时，输出的格式是多索引格式：

In [7]:

```python
countries_reviewed = reviews.groupby(['country', 'province']).description.agg([len])
countries_reviewed
```

Out[7]:

|           |                  | len  |
| :-------- | :--------------- | :--- |
| country   | province         |      |
| Argentina | Mendoza Province | 3264 |
| Other     | 536              |      |
| ...       | ...              | ...  |
| Uruguay   | San Jose         | 3    |
| Uruguay   | 24               |      |

425 rows × 1 columns



#### 4.2.1 单行索引reset_index()

但有时我们不想要使用多索引，而是想要使用单行索引，我们的方法是reset_index()：

In [9]:

```python
countries_reviewed.reset_index()
```

Out[9]:

|      | country   | province         | len  |
| :--- | :-------- | :--------------- | :--- |
| 0    | Argentina | Mendoza Province | 3264 |
| 1    | Argentina | Other            | 536  |
| ...  | ...       | ...              | ...  |
| 423  | Uruguay   | San Jose         | 3    |
| 424  | Uruguay   | Uruguay          | 24   |

425 rows × 3 columns



### 4.3 排序

#### 4.3.1 使用指定值排序

在默认的groupby输出中，数据使用索引排序，所以为了按照我们自己的想法排序，需要使用sort_values()函数：

sort_values函数默认是使用升序排列的，但是可以通过改变ascending参数使其为将排序

In [11]:

```python
countries_reviewed = countries_reviewed.reset_index()
countries_reviewed.sort_values(by='len', ascending=False)
```

Out[11]:

|      | country | province   | len   |
| :--- | :------ | :--------- | :---- |
| 392  | US      | California | 36247 |
| 415  | US      | Washington | 8639  |
| ...  | ...     | ...        | ...   |
| 63   | Chile   | Coelemu    | 1     |
| 149  | Greece  | Beotia     | 1     |

425 rows × 3 columns



#### 4.3.2 使用索引排序sort_index()

In [12]:

```
countries_reviewed.sort_index()
```

Out[12]:

|      | country   | province         | len  |
| :--- | :-------- | :--------------- | :--- |
| 0    | Argentina | Mendoza Province | 3264 |
| 1    | Argentina | Other            | 536  |
| ...  | ...       | ...              | ...  |
| 423  | Uruguay   | San Jose         | 3    |
| 424  | Uruguay   | Uruguay          | 24   |

425 rows × 3 columns



使用其他参数排序：

In [13]:

```python
countries_reviewed.sort_values(by=['country', 'len'])
```

Out[13]:

|      | country   | province         | len  |
| :--- | :-------- | :--------------- | :--- |
| 1    | Argentina | Other            | 536  |
| 0    | Argentina | Mendoza Province | 3264 |
| ...  | ...       | ...              | ...  |
| 424  | Uruguay   | Uruguay          | 24   |
| 419  | Uruguay   | Canelones        | 43   |

425 rows × 3 columns





## 5.Data Types and Missing Values



### 5.1 Dtypes:获取数据类型

In[2]:

```python
reviews.price.dtype
```

Out[2]:

```
dtype('float64')
```

In [3]:

```python
reviews.dtypes
```

Out[3]:

```
country        object
description    object
                ...  
variety        object
winery         object
Length: 13, dtype: object
```



### 5.2 astype()更改数据类型

In [4]:

```python
reviews.points.astype('float64')
```

Out[4]:

```
0         87.0
1         87.0
          ... 
129969    90.0
129970    90.0
Name: points, Length: 129971, dtype: float64
```



### 5.3 缺失值

缺失值一般被给予NaN值，意思是Not a Number

In [6]:

```python
reviews[pd.isnull(reviews.country)]
```

Out[6]:

|        | country | description                                       | designation    | points | price | province | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                          | variety   | winery             |
| :----- | :------ | :------------------------------------------------ | :------------- | :----- | :---- | :------- | :------- | :------- | :------------ | :-------------------- | :--------------------------------------------- | :-------- | :----------------- |
| 913    | NaN     | Amber in color, this wine has aromas of peach ... | Asureti Valley | 87     | 30.0  | NaN      | NaN      | NaN      | Mike DeSimone | @worldwineguys        | Gotsa Family Wines 2014 Asureti Valley Chinuri | Chinuri   | Gotsa Family Wines |
| 3131   | NaN     | Soft, fruity and juicy, this is a pleasant, si... | Partager       | 83     | NaN   | NaN      | NaN      | NaN      | Roger Voss    | @vossroger            | Barton & Guestier NV Partager Red              | Red Blend | Barton & Guestier  |
| ...    | ...     | ...                                               | ...            | ...    | ...   | ...      | ...      | ...      | ...           | ...                   | ...                                            | ...       | ...                |
| 129590 | NaN     | A blend of 60% Syrah, 30% Cabernet Sauvignon a... | Shah           | 90     | 30.0  | NaN      | NaN      | NaN      | Mike DeSimone | @worldwineguys        | Büyülübağ 2012 Shah Red                        | Red Blend | Büyülübağ          |
| 129900 | NaN     | This wine offers a delightful bouquet of black... | NaN            | 91     | 32.0  | NaN      | NaN      | NaN      | Mike DeSimone | @worldwineguys        | Psagot 2014 Merlot                             | Merlot    | Psagot             |

63 rows × 13 columns

#### 5.3.1 更改缺失值：.fillna()

使用.fillna()函数可以更改缺失值的值

In [7]:

```
reviews.region_2.fillna("Unknown")
```

Out[7]:

```
0         Unknown
1         Unknown
           ...   
129969    Unknown
129970    Unknown
Name: region_2, Length: 129971, dtype: object
```



#### 5.3.2 指定缺失值并更改：.replace()

前面的值是指定的要修改的值选项，后面这个值是值修改后的值

In [8]:

```python
reviews.taster_twitter_handle.replace("@kerinokeefe", "@kerino")
```

Out[8]:

```
0            @kerino
1         @vossroger
             ...    
129969    @vossroger
129970    @vossroger
Name: taster_twitter_handle, Length: 129971, dtype: object
```



## 6.Renaming and Combining

修改列的名字和联合数据

### 6.1 重命名rename()

讲points列的名字修改为score

In [2]:

```python
reviews.rename(columns={'points': 'score'})
```

Out[2]:

|        | country  | description                                       | designation                   | score | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety        | winery               |
| :----- | :------- | :------------------------------------------------ | :---------------------------- | :---- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| 0      | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | 87    | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia              |
| 1      | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                      | 87    | 15.0  | Douro             | NaN      | NaN      | Roger Voss    | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos  |
| ...    | ...      | ...                                               | ...                           | ...   | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...            | ...                  |
| 129969 | France   | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90    | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970 | France   | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90    | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

129971 rows × 13 columns





使用python中的字典模式来修改索引

In [3]:

```python
reviews.rename(index={0: 'firstEntry', 1: 'secondEntry'})
```

Out[3]:

|             | country  | description                                       | designation                   | points | price | province          | region_1 | region_2 | taster_name   | taster_twitter_handle | title                                             | variety        | winery               |
| :---------- | :------- | :------------------------------------------------ | :---------------------------- | :----- | :---- | :---------------- | :------- | :------- | :------------ | :-------------------- | :------------------------------------------------ | :------------- | :------------------- |
| firstEntry  | Italy    | Aromas include tropical fruit, broom, brimston... | Vulkà Bianco                  | 87     | NaN   | Sicily & Sardinia | Etna     | NaN      | Kerin O’Keefe | @kerinokeefe          | Nicosia 2013 Vulkà Bianco (Etna)                  | White Blend    | Nicosia              |
| secondEntry | Portugal | This is ripe and fruity, a wine that is smooth... | Avidagos                      | 87     | 15.0  | Douro             | NaN      | NaN      | Roger Voss    | @vossroger            | Quinta dos Avidagos 2011 Avidagos Red (Douro)     | Portuguese Red | Quinta dos Avidagos  |
| ...         | ...      | ...                                               | ...                           | ...    | ...   | ...               | ...      | ...      | ...           | ...                   | ...                                               | ...            | ...                  |
| 129969      | France   | A dry style of Pinot Gris, this is crisp with ... | NaN                           | 90     | 32.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Marcel Deiss 2012 Pinot Gris (Alsace)     | Pinot Gris     | Domaine Marcel Deiss |
| 129970      | France   | Big, rich and off-dry, this is powered by inte... | Lieu-dit Harth Cuvée Caroline | 90     | 21.0  | Alsace            | Alsace   | NaN      | Roger Voss    | @vossroger            | Domaine Schoffit 2012 Lieu-dit Harth Cuvée Car... | Gewürztraminer | Domaine Schoffit     |

129971 rows × 13 columns



### 6.2 联合数据

大致有三中方法：concat()、join()和merge()

#### 6.2.1 concat()函数：

类似于堆叠表格，既可以上下拼接（默认），也可以左右拼接

```python
df1 = pd.DataFrame({'A': [1, 2]})
df2 = pd.DataFrame({'A': [3, 4]})

result = pd.concat([df1, df2])
print(result)

>>>
   A
0  1
1  2
0  3
1  4

df3 = pd.DataFrame({'A': [1, 2]})
df4 = pd.DataFrame({'B': [3, 4]})

result = pd.concat([df3, df4], axis=1)
print(result)

>>>
   A  B
0  1  3
1  2  4
```



#### 6.2.2 join()函数

把两个DataFrame按索引对齐合并，默认是左连接，即保留左边表所有的索引，如果右边表没有对应的数据则用NaN填充

```python
import pandas as pd

df1 = pd.DataFrame({'A': [1, 2, 3]}, index=['x', 'y', 'z'])
df2 = pd.DataFrame({'B': [4, 5, 6]}, index=['x', 'y', 'w'])

# 按索引合并
result = df1.join(df2)
print(result)

# 由于是以df1为主的join函数，所以结果中，z索引在B列是没有值的，故为NaN
>>>
   A    B
x  1  4.0
y  2  5.0
z  3  NaN
```



# 五.Intermediate Machine Learning

中级的机器学习，这个系列主要是处理缺失的值、非数字值、数据泄露等

## 1.Introduction

在本次课程，我们将会学到：

- 处理那些经常在真实世界出现的数据类型(缺失值、可变变量等)
- 设计流水线工作流提升机器学习代码的质量
- 使用高级技术进行模型验证(例如交叉验证等)
- 建立最好的模型，这些模型被广泛的应用于kaggle比赛(如XGBoost等)
- 避免普通的和重要的数据科学错误(数据泄露等)



## 2.Missing Values

由于缺失数据在数据集中是非常常见的一种现象，比如两间卧室的房子不会包含第三间卧室的价格...

这章将会介绍三种处理丢失数据的方法



### 2.1 丢掉有缺失值的列

除非大多数的值在被丢失的列中是空值，否则不要这样做

![tut2_approach1](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/Sax80za.png)

```python
# Get names of columns with missing values
cols_with_missing = [col for col in X_train.columns
                     if X_train[col].isnull().any()]

# Drop columns in training and validation data
reduced_X_train = X_train.drop(cols_with_missing, axis=1)
reduced_X_valid = X_valid.drop(cols_with_missing, axis=1)

print("MAE from Approach 1 (Drop columns with missing values):")
print(score_dataset(reduced_X_train, reduced_X_valid, y_train, y_valid))
```



### 2.2 插补值

可以在缺失值内补值。一般补的是**平均值**

这样输入值在大多数情况下并不会是极其好的选择，但是他经常会得到更好的效果

![tut2_approach2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4BpnlPA.png)

```python
from sklearn.impute import SimpleImputer

# Imputation
my_imputer = SimpleImputer()
imputed_X_train = pd.DataFrame(my_imputer.fit_transform(X_train))
imputed_X_valid = pd.DataFrame(my_imputer.transform(X_valid))

# Imputation removed column names; put them back
imputed_X_train.columns = X_train.columns
imputed_X_valid.columns = X_valid.columns

print("MAE from Approach 2 (Imputation):")
print(score_dataset(imputed_X_train, imputed_X_valid, y_train, y_valid))
```



### 2.3 插补的延申

插补值法是一个标注的作法，并且这个方法经常工作的很好。但是插补的值可能与实际系统的值有偏差，或者带有缺失值的行可能是独一无二的在一些其他的情况。在这种情况下，我们的模型可以工作的更好通过识别哪些值是原始丢失的。

在一些情况下，这将显著的提升结果；在其他情况下，他可能没什么帮助

![tut3_approach3](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/UWOyg4a.png)

```python
# Make copy to avoid changing original data (when imputing)
X_train_plus = X_train.copy()
X_valid_plus = X_valid.copy()

# Make new columns indicating what will be imputed
for col in cols_with_missing:
    X_train_plus[col + '_was_missing'] = X_train_plus[col].isnull()
    X_valid_plus[col + '_was_missing'] = X_valid_plus[col].isnull()

# Imputation
my_imputer = SimpleImputer()
imputed_X_train_plus = pd.DataFrame(my_imputer.fit_transform(X_train_plus))
imputed_X_valid_plus = pd.DataFrame(my_imputer.transform(X_valid_plus))

# Imputation removed column names; put them back
imputed_X_train_plus.columns = X_train_plus.columns
imputed_X_valid_plus.columns = X_valid_plus.columns

print("MAE from Approach 3 (An Extension to Imputation):")
print(score_dataset(imputed_X_train_plus, imputed_X_valid_plus, y_train, y_valid))
```



## 3.Categorical Variables

分类数据只采用有限数量的值，在使用机器学习算法前，需要对分类数据进行预处理，大致有三种方法处理分类数据

下面例子挑选出的数据如下，已经排除有缺失值的列，并只保留类别数<10的列

|       | Type | Method | Regionname            | Rooms | Distance | Postcode | Bedroom2 | Bathroom | Landsize | Lattitude | Longtitude | Propertycount |
| :---- | :--- | :----- | :-------------------- | :---- | :------- | :------- | :------- | :------- | :------- | :-------- | :--------- | :------------ |
| 12167 | u    | S      | Southern Metropolitan | 1     | 5.0      | 3182.0   | 1.0      | 1.0      | 0.0      | -37.85984 | 144.9867   | 13240.0       |
| 6524  | h    | SA     | Western Metropolitan  | 2     | 8.0      | 3016.0   | 2.0      | 2.0      | 193.0    | -37.85800 | 144.9005   | 6380.0        |
| 8413  | h    | S      | Western Metropolitan  | 3     | 12.6     | 3020.0   | 3.0      | 1.0      | 555.0    | -37.79880 | 144.8220   | 3755.0        |
| 2919  | u    | SP     | Northern Metropolitan | 3     | 13.0     | 3046.0   | 3.0      | 1.0      | 265.0    | -37.70830 | 144.9158   | 8870.0        |
| 6043  | h    | S      | Western Metropolitan  | 3     | 13.3     | 3020.0   | 3.0      | 1.0      | 673.0    | -37.76230 | 144.8272   | 4217.0        |



```python
# Get list of categorical variables
s = (X_train.dtypes == 'object')
object_cols = list(s[s].index)

print("Categorical variables:")
print(object_cols)
```



### 3.1 移除分类数据

最简单的方法自然是去除这些分类数据，这样做的话，仅仅在列不包含有用的信息的时候有效果

```python
drop_X_train = X_train.select_dtypes(exclude=['object'])
drop_X_valid = X_valid.select_dtypes(exclude=['object'])

print("MAE from Approach 1 (Drop categorical variables):")
print(score_dataset(drop_X_train, drop_X_valid, y_train, y_valid))
```



### 3.2 序列编码

序列编码将给每一个值一个独一无二的整数，但是这样编码是因为单词之间有内在联系："Never" (0) < "Rarely" (1) < "Most days" (2) < "Every day" (3)，但并不是所有的分类数据都有这样的内在联系：

这种编码存在另外一种问题，即训练集种的标签与验证集的标签不匹配，可能验证集有的训练集没有

![tut3_ordinalencode](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/tEogUAr.png)

```python
from sklearn.preprocessing import OrdinalEncoder

# Make copy to avoid changing original data 
label_X_train = X_train.copy()
label_X_valid = X_valid.copy()

# Apply ordinal encoder to each column with categorical data
ordinal_encoder = OrdinalEncoder()
label_X_train[object_cols] = ordinal_encoder.fit_transform(X_train[object_cols])
label_X_valid[object_cols] = ordinal_encoder.transform(X_valid[object_cols])

print("MAE from Approach 2 (Ordinal Encoding):") 
print(score_dataset(label_X_train, label_X_valid, y_train, y_valid))
```



### 3.3 独热编码

但是独热编码在种类变多时并不会工作的很好(一般超过15个分类时就不会这样做了)



![tut3_onehot](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/TW5m0aJ.png)



```python
from sklearn.preprocessing import OneHotEncoder

# Apply one-hot encoder to each column with categorical data
OH_encoder = OneHotEncoder(handle_unknown='ignore', sparse=False)
OH_cols_train = pd.DataFrame(OH_encoder.fit_transform(X_train[object_cols]))
OH_cols_valid = pd.DataFrame(OH_encoder.transform(X_valid[object_cols]))

# One-hot encoding removed index; put it back
OH_cols_train.index = X_train.index
OH_cols_valid.index = X_valid.index

# Remove categorical columns (will replace with one-hot encoding)
num_X_train = X_train.drop(object_cols, axis=1)
num_X_valid = X_valid.drop(object_cols, axis=1)

# Add one-hot encoded columns to numerical features
OH_X_train = pd.concat([num_X_train, OH_cols_train], axis=1)
OH_X_valid = pd.concat([num_X_valid, OH_cols_valid], axis=1)

# Ensure all columns have string type
OH_X_train.columns = OH_X_train.columns.astype(str)
OH_X_valid.columns = OH_X_valid.columns.astype(str)

print("MAE from Approach 3 (One-Hot Encoding):") 
print(score_dataset(OH_X_train, OH_X_valid, y_train, y_valid))
```



## 4.Pipelines

流水线工作是一个简单的方式保持我们的数据预处理和生成模型代码，简单来说，管道绑定了预处理和模型生成步骤，以便你能够使用单一步骤去建立整个捆绑操作，管道操作有以下好处：

- 更简洁的代码：在预处理的每个步骤种操作数据可能会变得混，使用pipeline，我们将不需要在每一步中都跟中训练集和验证机数据
- 更少的bugs：有更少的机会误用一步或忘记一个预处理的步骤
- 更容易生产化
- 模型验证的更多选择



导入数据后如下：数据包含了分类值和缺失值的列，我们使用pipeline，是很容易解决这些问题的

In [2]:

```
X_train.head()
```

Out[2]:

|       | Type | Method | Regionname            | Rooms | Distance | Postcode | Bedroom2 | Bathroom | Car  | Landsize | BuildingArea | YearBuilt | Lattitude | Longtitude | Propertycount |
| :---- | :--- | :----- | :-------------------- | :---- | :------- | :------- | :------- | :------- | :--- | :------- | :----------- | :-------- | :-------- | :--------- | :------------ |
| 12167 | u    | S      | Southern Metropolitan | 1     | 5.0      | 3182.0   | 1.0      | 1.0      | 1.0  | 0.0      | NaN          | 1940.0    | -37.85984 | 144.9867   | 13240.0       |
| 6524  | h    | SA     | Western Metropolitan  | 2     | 8.0      | 3016.0   | 2.0      | 2.0      | 1.0  | 193.0    | NaN          | NaN       | -37.85800 | 144.9005   | 6380.0        |
| 8413  | h    | S      | Western Metropolitan  | 3     | 12.6     | 3020.0   | 3.0      | 1.0      | 1.0  | 555.0    | NaN          | NaN       | -37.79880 | 144.8220   | 3755.0        |
| 2919  | u    | SP     | Northern Metropolitan | 3     | 13.0     | 3046.0   | 3.0      | 1.0      | 1.0  | 265.0    | NaN          | 1995.0    | -37.70830 | 144.9158   | 8870.0        |
| 6043  | h    | S      | Western Metropolitan  | 3     | 13.3     | 3020.0   | 3.0      | 1.0      | 2.0  | 673.0    | 673.0        | 1970.0    | -37.76230 | 144.8272   | 4217.0        |



接下来我们使用三部定义完整的pipeline工作流程

### 4.1 步骤一：定义预处理步骤

**数值特征**：缺失值 → 填充为常数

**类别特征**：缺失值 → 用众数填充 → 独热编码

**整体流程**：按列分组，分别预处理，最后合并数据输出

```python
from sklearn.compose import ColumnTransformer # 用于对不同的列(特征)采用不同的预处理方式
from sklearn.pipeline import Pipeline		  # 便于把多个数据预处理步骤串联起来，形成一个数据处理流水线
from sklearn.impute import SimpleImputer	  # 用于填补数据中的缺失值
from sklearn.preprocessing import OneHotEncoder	# 用于把分类特征进行独热编码

# Preprocessing for numerical data
numerical_transformer = SimpleImputer(strategy='constant') # 对数字缺失值填补为0

# Preprocessing for categorical data
categorical_transformer = Pipeline(steps=[			# 对类别特征的缺失值用众数填补->对分类变量进行独热编码并忽略新类别
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

# Bundle preprocessing for numerical and categorical data	# 将操作打包
preprocessor = ColumnTransformer(
    transformers=[		# num和cat分别是numerical和categorical转换器的缩写，方便后续访问
        ('num', numerical_transformer, numerical_cols),
        ('cat', categorical_transformer, categorical_cols)
    ])
```



### 4.2 步骤二：定义模型

定义随机树模型：

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(n_estimators=100, random_state=0)
```



### 4.3 步骤三：创建和评估pipeline

最后，我们使用pipeline类定义一个类，打包预处理和模型步骤，有一些重要的事情需要注意：

- 使用Pipeline，我们预处理数据和拟合模型在一个单行代码中
- 使用Pipeline，我们将X_valid中未处理的特征提供给predict()命令，Pipeline会在生成预测之前自动预处理这些特征

```python
from sklearn.metrics import mean_absolute_error

# Bundle preprocessing and modeling code in a pipeline
my_pipeline = Pipeline(steps=[('preprocessor', preprocessor),
                              ('model', model)
                             ])

# Preprocessing of training data, fit model 
my_pipeline.fit(X_train, y_train)

# Preprocessing of validation data, get predictions
preds = my_pipeline.predict(X_valid)

# Evaluate the model
score = mean_absolute_error(y_valid, preds)
print('MAE:', score)
```



## 5.Cross-Validation

这是一个更好的方式来验证模型



机器学习是一个反复迭代的过程，在下面这个例子中，模型先以1st fold为验证集，其他fold为训练集进行训练，然后再以2st fold为验证集，其他fold为测试集进行训练，反复迭代5次

![tut5_crossval](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/9k60cVA.png)



- 对于小的数据集，可以使用交叉验证进行训练
- 对于大的数据集，可以使用80%train+20%valid的原始方法进行训练



```python
from sklearn.ensemble import RandomForestRegressor
from sklearn.pipeline import Pipeline
from sklearn.impute import SimpleImputer

my_pipeline = Pipeline(steps=[('preprocessor', SimpleImputer()),
                              ('model', RandomForestRegressor(n_estimators=50,
                                                              random_state=0))
                             ])


from sklearn.model_selection import cross_val_score

# Multiply by -1 since sklearn calculates *negative* MAE
scores = -1 * cross_val_score(my_pipeline, X, y,	# 交叉验证5次
                              cv=5,
                              scoring='neg_mean_absolute_error')	# 使用负均值绝对误差作为评分指标

print("MAE scores:\n", scores)
```



## 6.XGBoost

在本次课中，我们将学会如何使用梯度提升构建和优化模型，我们将随机森林方法叫做集成法，根据定义，集成法结合了许多模型预测，

在本次课中，我们将学习另外一种集成法，这个就叫做gradient boosting

梯度提升是一个将模型添加到一个整体，循环迭代的方法：

![tut6_boosting](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/MvCGENh.png)

首先，他使用一个单一模型初始化整体，虽然开始的这个模型预测可能是错误的，但是随后的整体增加将会解决这些错误

- 首先，我们使用现在的整体去生成预测对于数据集中的观测，为了做一个预测，我们从整体中的全部模型添加预测
- 这些预测被使用来计算损失函数
- 然后我们使用损失函数拟合一个新的模型，然后将其添加到整体中，特殊的是，我们决定模型的参数以便添加这个新的模型将会减少损失函数的值，在这里我们将使用梯度下降来实现损失函数的减少
- 最后，我们添加新的模型到整体中....不断迭代



```python
from xgboost import XGBRegressor

my_model = XGBRegressor()
my_model.fit(X_train, y_train)

from sklearn.metrics import mean_absolute_error

predictions = my_model.predict(X_valid)
print("Mean Absolute Error: " + str(mean_absolute_error(predictions, y_valid)))
```



### 6.1 参数选择

XGBoost有一些参数可以戏剧性的影像准确性和训练速度，第一个应该理解的参数是：

#### n_estimators：循环次数

n_estimator指定完成上述建模周期的次数，它等于我们在集成中包含的模型数量

- 太小的值会造成欠拟合
- 太大的值会造成过拟合

一般来说，取值在100~1000之间是比较好的选择，这依赖于学习率的大小

```python
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train)
```



#### early_stopping_rounds：最早停止循环

early_stopping_rounds提供了一个自动发现n_estimators理想值的方式，提前停止迭代会导致模型找不到最优解，明智的做法是设置n_estimators为一个较高的值，然后使用early_stopping_rounds来查找停止迭代的最佳时间。一般来说，early_stopping_rounds=5是一个合理的选择，在这种情况下，我们会在连续5论验证分数恶化后停止

在使用early_stopping_rounds时，我们还需要留出一些数据来计算验证分数，这是通过eval_set参数来完成的

```python
my_model = XGBRegressor(n_estimators=500)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)],
             verbose=False)
```



#### learning_rate：学习率

我们并不是将每个组件模型的预测相加来获得预测，而是将每个模型的预测乘以一个小数字(称为学习率)，然后再将他们相加

一般来说，较小的学习率和大量的估计器将产生更准确的XGBoost模型，尽管模型也需要更长的时间来训练，默认情况下，XGBoost将学习率设置为0.1



```python
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```



#### n_jobs：核数

在大型的数据集上，运行时间是一个需要考虑的事情，我们可以使用并行计算来改善运行时间，一般来说，我们设置n_jobs=机器核心数。在小型数据集上，这并不会有什么帮助，但是在大型数据集上，这将改善我们的计算速度

```python
my_model = XGBRegressor(n_estimators=1000, learning_rate=0.05, n_jobs=4)
my_model.fit(X_train, y_train, 
             early_stopping_rounds=5, 
             eval_set=[(X_valid, y_valid)], 
             verbose=False)
```





## 7.Data Leakage

数据泄露发生在当你的训练数据包含目标信息的时候，但是相似的信息并不会变成有用的当模型被用来预测，这使得模型在训练集(甚至验证集)上表现的很好，但是在预测时将表现的很差

有两种主要的泄露类型：**目标泄露**和**训练-测试污染** 



### 7.1 目标泄露

模型提前看到了不该有的"答案"，例子：

| got_pneumonia | age  | weight | male  | took_antibiotic_medicine | ...  |
| :-----------: | :--: | :----: | :---: | :----------------------: | :--- |
|     False     |  65  |  100   | False |          False           | ...  |
|     False     |  72  |  130   | True  |          False           | ...  |
|     True      |  58  |  100   | False |           True           | ...  |

我们现在想预测谁将会染上肺炎，如果使用上列数据将会发现，吃抗生素药和染上肺炎之间有强相关，但是在真实世界预测时，我们无法使用这个模型，因为病人一般只有在染上肺炎之后才吃药，而不是吃了药才不染上肺炎



### 7.2 训练-测试污染

训练集和测试集信息混杂

测试集意味着是一种测量模型性能的方式，使用训练时没出现的数据，但是如果验证的数据在训练前就已经被“看到”了，那么会产生污染





### 7.3 示例

我们将使用下面的数据集来进行测试，y是信用卡的申请，X如下，我们将使用它来进行哪些申请将会被通过

|      | reports | age      | income | share    | expenditure | owner | selfemp | dependents | months | majorcards | active |
| :--- | :------ | :------- | :----- | :------- | :---------- | :---- | :------ | :--------- | :----- | :--------- | :----- |
| 0    | 0       | 37.66667 | 4.5200 | 0.033270 | 124.983300  | True  | False   | 3          | 54     | 1          | 12     |
| 1    | 0       | 33.25000 | 2.4200 | 0.005217 | 9.854167    | False | False   | 3          | 34     | 1          | 13     |
| 2    | 0       | 33.66667 | 4.5000 | 0.004156 | 15.000000   | True  | False   | 4          | 58     | 1          | 5      |
| 3    | 0       | 30.50000 | 2.5400 | 0.065214 | 137.869200  | False | False   | 0          | 25     | 1          | 7      |
| 4    | 0       | 32.16667 | 9.7867 | 0.067051 | 546.503300  | True  | False   | 2          | 64     | 1          | 5      |

导入数据

```python
import pandas as pd

# Read the data
data = pd.read_csv('../input/aer-credit-card-data/AER_credit_card_data.csv', 
                   true_values = ['yes'], false_values = ['no'])

# Select target
y = data.card

# Select predictors
X = data.drop(['card'], axis=1)

print("Number of rows in the dataset:", X.shape[0])
X.head()
```

进行预测

```python
from sklearn.pipeline import make_pipeline
from sklearn.ensemble import RandomForestClassifier
from sklearn.model_selection import cross_val_score

# Since there is no preprocessing, we don't need a pipeline (used anyway as best practice!)
my_pipeline = make_pipeline(RandomForestClassifier(n_estimators=100))
cv_scores = cross_val_score(my_pipeline, X, y, 
                            cv=5,
                            scoring='accuracy')

print("Cross-validation accuracy: %f" % cv_scores.mean())

>>> Cross-validation accuracy: 0.981052
```

我们发现，在验证集上的准确率达到了惊人的98%，这是不正常的，仔细观察X数据集，我们发现，expenditure应该是申请了信用卡后每个月的输出，share、active、majorcards等变量都有同样的问题，所以应该在训练时舍弃这些数据

```python
# Drop leaky predictors from dataset
potential_leaks = ['expenditure', 'share', 'active', 'majorcards']
X2 = X.drop(potential_leaks, axis=1)

# Evaluate the model with leaky predictors removed
cv_scores = cross_val_score(my_pipeline, X2, y, 
                            cv=5,
                            scoring='accuracy')

print("Cross-val accuracy: %f" % cv_scores.mean())

>>> Cross-val accuracy: 0.830919
```



# 六.Data Visualization





# 七.Feature Engineering



## 1.What Is Feature Engineering

在本课中，我们将学到

- 使用交互信息决定哪一个特征是最重要的
- 发行新的特征，在几个真实世界的领域要求上
- 使用目标编码对高基数分类进行编码
- 使用 K-Means 聚类创建细分特征
- 使用主成分分析将数据集的变体分解为特征















