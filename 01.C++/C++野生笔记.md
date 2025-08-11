# **一.C++基础入门**

## 1.C++基本常识

1）计算机的基本单元是位(bit)

字节通常指的是8位的内存单元，1KB=1024字节，1MB=1024KB

2）科学表达式：2.52e+8=2.52 * 10^8 ,  8.33e-4=8.83 * 10^(-8)

3）计算机存储数据时必须跟踪的3种基本属性：

- 1.信息存储在何处

- 2.存储的值为多少

- 3.存储的信息是什么类型

4）Visual Studio中一个项目包含多个源文件的方法：

右键—>属性—>从生成中移除—>是—>应用—>确定。

5）多行注释：

选中：**ctrl+k与crtl+c**

取消：**crtl+k与crtl+u**

6）随机数生成：

```c++
#include <iostream>
#include <ctime>
int main()
{
    srand((unsigned int)time(NULL));
    int random=rand()%60+40;//40~99
    return 0;
}
```



### 1.1 所有的C++代码必须有的步骤前提：

```c++
#include <iostream>
using namespace std;

int main()
{
    
    system("pause");
    
    return 0;
    
}
```

#include预处理器指令的主要功能是在编译器进行源代码的编译过程之前，添加或者替换相应的预编译指令，从而使得用户源代码中调用的系统预定义函数和各种标识符能够正确地被编码器识别和编译。iostream头文件主要包含了系统的标准输入/输出函数以及数据的声明和定义

using预编译指令的主要功能是表明当前源代码文件使用的名称空间std。

#### 1.1.1 创建项目

​	Visual Studio是我们用来编写C++程序的主要工具，我们先将它打开

![1541383178746](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1541383178746.png)



![1541384366413](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1541384366413.png)

#### 1.1.2 创建文件

右键源文件，选择添加->新建项

![1541383817248](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1541383817248.png)

给C++文件起个名称，然后点击添加即可。

![1541384140042](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1541384140042.png)

### 1.2 C++输出语句：

```c++
cout<<"内容"<<endl;
```

endl的作用是换行，有时也可以用/n来代替。

（符号>>和<<都代表的是信息流的方向）

### 1.3 C++注释语句：

```c++
单行注释：//注释内容
多行注释：/* 注释内容*/
```

### 1.4 C++变量定义：

数据类型 变量名 =初始值；

==C++在创建变量时，必须给变量一个初始值，否则会报错==。

```c++
int a = 10;
```

1）变量定义时，变量名称中只能使用字母字符、数字和下划线_。

2）名称的==第一个字符不能是数字==

3）变量的名称区分大写字符与小写字符



### 1.5 常量的定义：

常用形式：

```c++
1.#define 常量名 常量值
2.const 数据类型 常量名 = 常量值;
```

1）define变量在main函数前定义，==且句尾没有分号==，const定义在main函数内，==且句尾有分号==。

2）const变量和define变量定义后==都不可以改变定义值==。

3）不要用关键字做为变量和常量名。

关键字：

| asm        | do           | if               | return      | typedef  |
| ---------- | ------------ | ---------------- | ----------- | -------- |
| auto       | double       | inline           | short       | typeid   |
| bool       | dynamic_cast | int              | signed      | typename |
| break      | else         | long             | sizeof      | union    |
| case       | enum         | mutable          | static      | unsigned |
| catch      | explicit     | namespace        | static_cast | using    |
| char       | export       | new              | struct      | virtual  |
| class      | extern       | operator         | switch      | void     |
| const      | false        | private          | template    | volatile |
| const_cast | float        | protected        | this        | wchar_t  |
| continue   | for          | public           | throw       | while    |
| default    | friend       | register         | true        |          |
| delete     | goto         | reinterpret_cast | try         |          |

### 1.6 标识符命名规则

1）标识符不能是关键字

2）标识符只能由==字母，数字，下划线==组成

3）第一个字符必须为==字母或下划线==

4）标识符中字符区分大小写





## 2.数据类型：

信息的存储需要三个基本属性：

1）信息将存储在哪里

2）要存储什么值

3）存储何种类型的信息



### 2.1 整型：

**作用**：整型变量表示的是整型类型的数据

**语法**：`short/int/long/long long	a	=10;`

整型的类型有以下几种，区别在于所占内存空间不同：

| **数据类型**        | **占用空间**                                    | 取值范围         |
| ------------------- | ----------------------------------------------- | ---------------- |
| short(短整型)       | 2字节                                           | (-2^15 ~ 2^15-1) |
| int(整型)           | 4字节                                           | (-2^31 ~ 2^31-1) |
| long(长整形)        | Windows为4字节，Linux为4字节(32位)，8字节(64位) | (-2^31 ~ 2^31-1) |
| long long(长长整形) | 8字节                                           | (-2^63 ~ 2^63-1) |

1）如果数据超过取值范围，会造成显示的结果不是正确的结果。

2）一般常用的是int类型。





### 2.2 sizeof关键字

**作用**：利用sizeof关键字可以统计数据类型==所占内存空间==的大小

**语法**： `siceof(数据类型/变量);`

示例：

```c++
cout << "short 类型所占内存空间为： " << sizeof(short) << endl;
cout << "int 类型所占内存空间为： " << sizeof(int) << endl;
cout << "long 类型所占内存空间为： " << sizeof(long) << endl;
cout << "long long 类型所占内存空间为： " << sizeof(long long) << endl;
```



sizeof(数组名)得到的是整个数组中的字节数

sizeof(数组元素)得到的是元素的长度



### 2.3 实型（浮点型）

**作用**：用于==表示小数==

**语法**：`float/double	f1/d1	=	3.14;`

浮点型变量一般分为两种：

1）单精度float

2）双精度double

二者的区别在于表示的有效数字范围不同。

| **数据类型** | **占用空间** | **有效数字范围** |
| ------------ | ------------ | ---------------- |
| float        | 4字节        | 7位有效数字      |
| double       | 8字节        | 15～16位有效数字 |

示例：

```c++
float f1 = 3.14f;	
double d1 = 3.14;
cout << f1 << endl;
cout << d1<< endl;
float f2 = 3e2; 	// 3 * 10 ^ 2 
cout << "f2 = " << f2 << endl;
float f3 = 3e-2;  	// 3 * 0.1 ^ 2
cout << "f3 = " << f3 << endl;
```

1）==float型变量最好在数字后+f==，这样系统才会认为变量是float型，否则系统会把变量自认为是double型。

2）浮点类型默认为double类型。

3）科学计数法：3e2 = 3*10^2

​							 3e-2 = 3*0.1^2





### 2.4 字符型

**作用**：字符型变量用于显示单个字符

**语法**：`char ch=	'a';`

注意1：在显示字符型变量时，用==单引号==将字符括起来，==不要用双引号==。

注意2：单引号内==只能有一个字符==，不可以是字符串。

1）C和C++中字符型变量只占用==1个字节==。

2）字符型变量并不是把字符本身放到内存中存储，而是将==对应的ASCII编码放入到存储单元==。

示例：

```c++
char ch = 'a';
cout << ch << endl;
cout << sizeof(char) << endl;
cout << (int)ch << endl; 	//查看字符a对应的ASCII码
ch = 97;					//可以直接用ASCII给字符型变量赋值
cout << ch << endl;
```

ASCII码表格：

| **ASCII**值 | **控制字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** | **ASCII**值 | **字符** |
| ----------- | ------------ | ----------- | -------- | ----------- | -------- | ----------- | -------- |
| 0           | NUT          | 32          | (space)  | 64          | @        | 96          | 、       |
| 1           | SOH          | 33          | !        | 65          | A        | 97          | a        |
| 2           | STX          | 34          | "        | 66          | B        | 98          | b        |
| 3           | ETX          | 35          | #        | 67          | C        | 99          | c        |
| 4           | EOT          | 36          | $        | 68          | D        | 100         | d        |
| 5           | ENQ          | 37          | %        | 69          | E        | 101         | e        |
| 6           | ACK          | 38          | &        | 70          | F        | 102         | f        |
| 7           | BEL          | 39          | ,        | 71          | G        | 103         | g        |
| 8           | BS           | 40          | (        | 72          | H        | 104         | h        |
| 9           | HT           | 41          | )        | 73          | I        | 105         | i        |
| 10          | LF           | 42          | *        | 74          | J        | 106         | j        |
| 11          | VT           | 43          | +        | 75          | K        | 107         | k        |
| 12          | FF           | 44          | ,        | 76          | L        | 108         | l        |
| 13          | CR           | 45          | -        | 77          | M        | 109         | m        |
| 14          | SO           | 46          | .        | 78          | N        | 110         | n        |
| 15          | SI           | 47          | /        | 79          | O        | 111         | o        |
| 16          | DLE          | 48          | 0        | 80          | P        | 112         | p        |
| 17          | DCI          | 49          | 1        | 81          | Q        | 113         | q        |
| 18          | DC2          | 50          | 2        | 82          | R        | 114         | r        |
| 19          | DC3          | 51          | 3        | 83          | S        | 115         | s        |
| 20          | DC4          | 52          | 4        | 84          | T        | 116         | t        |
| 21          | NAK          | 53          | 5        | 85          | U        | 117         | u        |
| 22          | SYN          | 54          | 6        | 86          | V        | 118         | v        |
| 23          | TB           | 55          | 7        | 87          | W        | 119         | w        |
| 24          | CAN          | 56          | 8        | 88          | X        | 120         | x        |
| 25          | EM           | 57          | 9        | 89          | Y        | 121         | y        |
| 26          | SUB          | 58          | :        | 90          | Z        | 122         | z        |
| 27          | ESC          | 59          | ;        | 91          | [        | 123         | {        |
| 28          | FS           | 60          | <        | 92          | /        | 124         | \|       |
| 29          | GS           | 61          | =        | 93          | ]        | 125         | }        |
| 30          | RS           | 62          | >        | 94          | ^        | 126         | `        |
| 31          | US           | 63          | ?        | 95          | _        | 127         | DEL      |

常用ASCII码：

1）A=65，a=97。

如何使用C++来找出编码88表示的字符？

```c++
char example = 88;
cout << example;
cout << char(88);
cout << (char)88;
```



### 2.5 转义字符

**作用**：用于表示一些==不能显示出来的ASCII字符==

现阶段常用的转义字符有：`\n  \\  \t`

| **转义字符** | **含义**                                | **ASCII**码值（十进制） |
| ------------ | --------------------------------------- | ----------------------- |
| \a           | 警报                                    | 007                     |
| \b           | 退格(BS) ，将当前位置移到前一列         | 008                     |
| \f           | 换页(FF)，将当前位置移到下页开头        | 012                     |
| **\n**       | **换行(LF) ，将当前位置移到下一行开头** | **010**                 |
| \r           | 回车(CR) ，将当前位置移到本行开头       | 013                     |
| **\t**       | **水平制表(HT)  （跳到下一个TAB位置）** | **009**                 |
| \v           | 垂直制表(VT)                            | 011                     |
| \ \          | **代表一个反斜线字符""**                | **092**                 |
| '            | 代表一个单引号（撇号）字符              | 039                     |
| "            | 代表一个双引号字符                      | 034                     |
| \?           | 代表一个问号                            | 063                     |
| \0           | 数字0                                   | 000                     |
| \ddd         | 8进制转义字符，d范围0~7                 | 3位8进制                |
| \xhh         | 16进制转义字符，h范围0~9，a~f，A~F      | 3位16进制               |

示例：

```c++
int main()
{
    cout<<"\\"<<endl;	//输出/字符
    cout<<"/tHello"<<endl;	//输出TAB的位置和Hello
    cout<<"\n"<<endl;	//换行
    
    system("pause");
    return 0;
}
```

### 2.6 字符串型

**作用**：用于表示一串字符

**语法**：有两种语法，C和C++

​			`C：char 变量名[] = "字符串值" `

​			`C++: string 变量名 = "字符串值"`

示例：

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
    char str1[] = "hello world";
    string str2 = "hello world";

    cout << str1 << endl;
    cout << str2 << endl;
    system("pause");
    return 0;
}
```

注意：1)使用string定义字符串时，需要在头文件处加上==#include <string>==这个头文件。

​			2)使用C的语法定义字符串时，别忘了==[]==。

​			3)string类型可以实现字符穿的赋值、拼接和附加。



### 2.7 布尔类型bool

**作用：**布尔数据类型代表真或假的值 

bool类型只有两个值：

* true  --- 真（本质是1）
* false --- 假（本质是0）

bool类型占1个字节的大小

示例：

```c++
int main()
{
    bool flag1 = true;
    cout << flag1 << endl;

    bool flag2 = false;
    cout << flag2 << endl;

    system("pause");
    return 0;
}
```

输出1和0.

### 2.8 数据的输入

**作用**：用于从键盘获取数据

**语法**：`cin >> 变量`

示例：

```c++
int main()
{
    //整型输入
    int a = 0;
    cout<<"请输入整型变量"<< endl;
    cin >> a;
    cout<< a << endl;
    
    //浮点型输入
    double d = 0;
    cout << "请输入浮点型变量："<< endl;
    cin >> d;
    cout << d << endl;
    
    //字符型输入
    char ch = 'a';
    cout <<"请输入字符型变量"<< endl;
    cin >> ch;
    cout << ch << endl;
    
    //字符串型输入
    string str = "hello";
    cout << "清输入字符串型变量" << endl;
    cin >> str;
    cout << str << endl;
    
    //布尔类型输入
    bool flag = true;
    cout << "请输入布尔型变量" << endl;
    cin >> flag ;
    cout << flag << endl;
    
    
    system("pause");
    return 0;
}
```

## 3.运算符

### 3.1 算术运算符

**作用**：用于处理四则运算

| **运算符** | **术语**   | **示例**    | **结果**  |
| ---------- | ---------- | ----------- | --------- |
| +          | 正号       | +3          | 3         |
| -          | 负号       | -3          | -3        |
| +          | 加         | 10 + 5      | 15        |
| -          | 减         | 10 - 5      | 5         |
| *          | 乘         | 10 * 5      | 50        |
| /          | 除         | 10 / 5      | 2         |
| %          | 取模(取余) | 10 % 3      | 1         |
| ++         | 前置递增   | a=2; b=++a; | a=3; b=3; |
| ++         | 后置递增   | a=2; b=a++; | a=3; b=2; |
| --         | 前置递减   | a=2; b=--a; | a=1; b=1; |
| --         | 后置递减   | a=2; b=a--; | a=1; b=2; |

注意：1）两个==整数相除结果仍然是整数==

​			2）除数不可以为0。

​			3）==只有整型变量可以进行取模运算==，两个小数不可以。

​			4）前置递增对变量先进行++，再计算表达式；后置递增先进性表达式运算，后让变量+1。对于类而言，前缀版本的效率比后缀版本高。

​			5）前缀递增、递减和解除引用*运算符优先级相同，以从右到左的方式进行结合。

​				  后缀递增、递减比前缀运算符的优先级高，这两个运算符以从左到右的方式进行结合。

示例：

```c++
int main()
{
    
    int a1 = 10;
    int b1 = ++a1 * 10;
    cout << a1 << endl;
    cout << b1 << endl;
	// a1=11,b1=110
    
    int a2 = 10;
    int b2 = a2++ * 10;
    cout << a2 << endl;
    cout << b2 << endl;
	// a2=11,b2=100
    
    system("pause");
    return 0;
}
```

### 3.2 赋值运算符

**作用**：用于将表达式的值赋给变量

| **运算符** | **术语** | **示例**   | **结果**  |
| ---------- | -------- | ---------- | --------- |
| =          | 赋值     | a=2; b=3;  | a=2; b=3; |
| +=         | 加等于   | a=0; a+=2; | a=2;      |
| -=         | 减等于   | a=5; a-=3; | a=2;      |
| *=         | 乘等于   | a=2; a*=2; | a=4;      |
| /=         | 除等于   | a=4; a/=2; | a=2;      |
| %=         | 模等于   | a=3; a%2;  | a=1;      |

可以理解为 a+=2与a=a+2是一个意思，其他同理

### 3.3 比较运算符

**作用：**用于表达式的比较，并返回一个真值或假值

| **运算符** | **术语** | **示例** | **结果** |
| ---------- | -------- | -------- | -------- |
| ==         | 相等于   | 4 == 3   | 0        |
| !=         | 不等于   | 4 != 3   | 1        |
| <          | 小于     | 4 < 3    | 0        |
| >          | 大于     | 4 > 3    | 1        |
| <=         | 小于等于 | 4 <= 3   | 0        |
| >=         | 大于等于 | 4 >= 1   | 1        |

示例：

```c++
int main() 
{
	int a = 10;
	int b = 20;

	cout << (a == b) << endl; // 0 

	cout << (a != b) << endl; // 1

	cout << (a > b) << endl; // 0

	cout << (a < b) << endl; // 1

	cout << (a >= b) << endl; // 0

	cout << (a <= b) << endl; // 1
	
	system("pause");

	return 0;
}
```

注意： 1）数字1表示真，数字0表示假

​			 2）在cout的输出中，==需要把（a!=b）这种运算括号起来==，否则报错

### 3.4 逻辑运算符

| **运算符** | **术语** | **示例** | **结果**                                                 |
| ---------- | -------- | -------- | -------------------------------------------------------- |
| !          | 非       | !a       | 如果a为假，则!a为真；  如果a为真，则!a为假。             |
| &&         | 与       | a && b   | 如果a和b都为真，则结果为真，否则为假。                   |
| \|\|       | 或       | a \|\| b | 如果a和b有一个为真，则结果为真，二者都为假时，结果为假。 |

1.||运算符先修改左侧的值，再对右侧的值进行判定。如果==左侧的表达式为true，则C++将不会去判断右侧的表达式==。

2.&&运算符如果==左侧为false，则右侧表达式将不会被判定与计算==。

3.优先级：and(&&)>or(||)>not(!)。

4.等号优先级非常小

## 4.程序流程结构

### 4.1选择结构

#### 4.1.1 if语句

**作用**：执行满足条件的语句

**语法**：`if() {} else {}`

注意：if()后不要加括号

1.if测试条件也将被强制转为bool值，因此0将被转换为false，非零为true。



#### 4.1.2 三木运算符

**作用：** 通过三目运算符实现简单的判断

**语法：**`表达式1 ? 表达式2 ：表达式3`

**解释：**

- 如果表达式1的值为真，执行表达式2，并返回表达式2的结果；


- 如果表达式1的值为假，执行表达式3，并返回表达式3的结果。




在C++中三目运算符返回的是变量，可以继续赋值。

示例：

```c++
int main ()
{
    int a = 10;
    int b = 20;
    int c = 0;
    c = (a > b ? a : b);
    cout << "c = " << c << endl;	// c = 20
    
    (a > b ? a : b) = 100;	//b= 100
    cout << "a = " << a << endl;	//a=10
    cout << "b = " << b << endl;	//b=100
    cout << "c = " << c << endl;	//c=20
    
    system("pause");
    return 0;
}
```



#### 4.1.3 switch 语句

**作用：**执行多条件分支语句

**语法：**

```C++
switch(表达式)

{

	case 结果1：执行语句;break;

	case 结果2：执行语句;break;

	...

	default:执行语句;break;

}

```

注意1 ：switch语句中表达式类型只能是整型或者字符型

注意2 ：case里如果没有break，那么程序会一直向下执行

注意3 ：与if语句相比，对于多条件判断时，switch的结构清晰，执行效率高，缺点是switch不可以判断区间。

### 4.2 循环结构

#### 4.2.1 while循环语句

**作用：**满足循环条件，执行循环语句

**语法：**` while(循环条件){ 循环语句 }`

```c++
#include <iostream>
using namespace std;
//time系统时间头文件包含
#include <ctime>
int main()
{
    //添加随机数种子，作用利用当前系统时间生成随机数，防止每次随机数都一样
    srand((unsigned int)time(NULL));
    int num1;
    int num2;
    //rand()生成随机数，然后求余
    num1 = rand()%100	//生成随机数0~99
    num2 = rand()%100+1	//生成随机数1~100
}
```

#### 4.2.2 do...while循环语句

**作用：** 满足循环条件，执行循环语句

**语法：** `do{ 循环语句 } while(循环条件);`

**注意：**与while的区别在于==do...while会先执行一次循环语句==，再判断循环条件

从水仙花数程序中得到的经验：

以153举例：

- 如果想获得个位数字，a=num%10;		//a=3


- 如果想获得十位数字，a=num/10%10;	//b=5,在定义的整型变量中，153/10的结果是15


- 如果想获得百位数字，a=num/100;		//c=1，在定义的整型变量中，153/100的结果是1




#### 4.2.3 for循环语句

**作用：** 满足循环条件，执行循环语句

**语法：**` for(起始表达式;条件表达式;末尾循环体) { 循环语句; }`

如果在语句块种定义一个新的变量，则仅当程序执行该语句块种的语句时，该变量才存在。执行完该语句块后，变量将被释放。



### 4.3 跳转语句

#### 4.3.1 break语句

**作用:** 用于跳出==选择结构==或者==循环结构==

break使用的时机：

* 出现在switch条件语句中，作用是终止case并跳出switch
* 出现在循环语句中，作用是跳出当前的循环语句
* 出现在嵌套循环中，跳出==最近的内层循==语句



#### 4.3.2 continue语句

**作用：**在==循环语句==中，跳过本次循环中余下尚未执行的语句，继续执行下一次循环

注意：break会跳出循环，而continue并没有使整个循环中止



#### 4.3.3 goto语句

**作用：**可以无条件跳转语句

**语法：** `goto 标记;`

注意：在程序中不建议使用goto语句，以免造成程序流程混乱。



## 5.数组

### 5.1 概述

**特点1：**数组中的每个==数据元素都是相同的数据类型==

**特点2：**数组是由==连续的内存==位置组成的

### 5.2 一维数组

#### 5.2.1一维数组定义方式

一维数组定义的三种方式：

1. ` 数据类型  数组名[ 数组长度 ]; `
2. `数据类型  数组名[ 数组长度 ] = { 值1，值2 ...};`
3. `数据类型  数组名[ ] = { 值1，值2 ...};`

注意：可以用以下代码获取一维数组的长度

```c++
int num = sizeof (数组名) / sizeof (数组名[0]);
```

函数strlen()只计算可见的字符，并不把空字符计算在内。

```c++
int a = strlen(Basicman)	/a=8
```

#### 5.2.2一维数组数组名

1.直接打印数组名，可以查看数组所存内存的首地址。

2.数组名是常量，不可以赋值。

示例：

```c++
cout << "数组首地址为： " << (int)arr << endl;
cout << "数组中第一个元素地址为： " << (int)&arr[0] << endl;
cout << "数组中第二个元素地址为： " << (int)&arr[1] << endl;
```

字符串数组输入时的潜在隐患：

```c++
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin >> name;
    cout << "Enter your favorite dessert:\n";
    cin >> dessert;
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
	// cin.get();
    return 0; 
}
```

如果输入的名字是 WANG CE，那么程序输出效果如下所示：

![TNFF2%CXLH`F9~1~GI0MO9D](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/TNFF2%CXLH`F91GI0MO9D.png)

很明显，与预期效果不符，原因解释：

==cin使用空白(空格、制表符和换行符)来确定字符串的结束位置，这意味着cin在获取字符串数组输入时只读取一个单词，Wang被输入到name数组中，而CE被自动输入到dessert数组中==

1）getline()函数读取整行，它使用通过回车键输入的换行符来确定输入结尾，第一个参数是用来存储输入行的数组的名称，第二个参数时要读取的字符数。代码示例：

```c++
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.getline(name, ArSize);  // reads through newline
    cout << "Enter your favorite dessert:\n";
    cin.getline(dessert, ArSize);
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
    return 0; 
}

```

结果：

![QQ图片20230314195541](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230314195541.png)

2）get()函数

```c++
#include <iostream>
int main()
{
    using namespace std;
    const int ArSize = 20;
    char name[ArSize];
    char dessert[ArSize];

    cout << "Enter your name:\n";
    cin.get(name, ArSize).get();    // read string, newline		//防止这行输入的回车键自动输入到下一行输入
    cout << "Enter your favorite dessert:\n";
    cin.get(dessert, ArSize).get();		
    cout << "I have some delicious " << dessert;
    cout << " for you, " << name << ".\n";
    // cin.get();
    return 0; 
}
```



#### 5.2.3冒泡排序

**作用：** 最常用的排序算法，对数组内元素进行排序

1. 比较相邻的元素。如果第一个比第二个大，就交换他们两个。
2. 对每一对相邻元素做同样的工作，执行完毕后，找到第一个最大值。
3. 重复以上的步骤，每次比较次数-1，直到不需要比较

示例：

```c++
#include <iostream>
#include <string>
using namespace std;
#include <ctime>

int main()
{
    int i ;  //定义轮数
    int j ;  //定义每轮对比次数
    int temp;   //定义暂存值
    int arr[] = { 4,2,8,0,5,7,1,3,9 };  //定义排序数组
    int num = sizeof(arr) / sizeof(arr[0]); //确定数组内元素个数
    
    cout << "排序前的数组为：" ;
    for (i = 0;i < num;i++)
    {
        cout << arr[i] ;
    }
    cout << endl;
    
    //排序轮数 = 元素个数 - 1 ；
    //每轮对比次数 = =元素个数 - 排序次数 - 1；
    for (i = 0;i < num - 1;i++)
    {
        for (j = 0;j < num - i - 1;j++)
        {
            if (arr[j] > arr[j + 1])
            {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    
    cout << "排序后的数组为：" ;
    for (i = 0;i < num;i++)
    {
        cout << arr[i];
    }
    cout << endl;

    system("pause");
    return 0;
}
```

重点：

- 排序轮数 = 元素个数 - 1 ；

- 每轮对比次数 = =元素个数 - 排序次数 - 1；

### 5.3 二维数组

#### 5.3.1二维数组的的定义方式：

1. ` 数据类型  数组名[ 行数 ][ 列数 ]; `
2. `数据类型  数组名[ 行数 ][ 列数 ] = { {数据1，数据2 } ，{数据3，数据4 } };`
3. `数据类型  数组名[ 行数 ][ 列数 ] = { 数据1，数据2，数据3，数据4};`
4. ` 数据类型  数组名[  ][ 列数 ] = { 数据1，数据2，数据3，数据4};`

最好选择第二种来定义二维数组。

定义二维数组代码：

```c++
#include <iostream>
#include <string>
using namespace std;
#include <ctime>

int main()
{
    int arr2[2][3] =
    {
        {1,2,3},
        {4,5,6}
    };
    int i = 0;
    int j = 0;
    for (i=0;i<2;i++)
    {
        for (j = 0;j < 3; j++)
        {
            cout << arr2[i][j] << " ";
        }
        cout << endl;
    }
    system("pause");
    return 0;
}
```

#### 5.3.2 二维数组数组名

1.查看二维数组所占内存空间

2.获取二维数组首地址

代码示例：

```c++
int main() {

	//二维数组数组名
	int arr[2][3] =
	{
		{1,2,3},
		{4,5,6}
	};

	cout << "二维数组大小： " << sizeof(arr) << endl;
	cout << "二维数组一行大小： " << sizeof(arr[0]) << endl;
	cout << "二维数组元素大小： " << sizeof(arr[0][0]) << endl;

	cout << "二维数组行数： " << sizeof(arr) / sizeof(arr[0]) << endl;
	cout << "二维数组列数： " << sizeof(arr[0]) / sizeof(arr[0][0]) << endl;

	//地址
	cout << "二维数组首地址：" << arr << endl;
	cout << "二维数组第一行地址：" << arr[0] << endl;
	cout << "二维数组第二行地址：" << arr[1] << endl;

	cout << "二维数组第一个元素地址：" << &arr[0][0] << endl;
	cout << "二维数组第二个元素地址：" << &arr[0][1] << endl;

	system("pause");

	return 0;
}
```

1.二维数组名就是这个数组的首地址

2.对二维数组名进行sizeof时，可以获得整个二维数组所占内存大小

#### **5.3.3 二维数组应用案例**

**考试成绩统计：**

案例描述：有三名同学（张三，李四，王五），在一次考试中的成绩分别如下表，**请分别输出三名同学的总成绩**

|      | 语文 | 数学 | 英语 |
| ---- | ---- | ---- | ---- |
| 张三 | 100  | 100  | 100  |
| 李四 | 90   | 50   | 100  |
| 王五 | 60   | 70   | 80   |

代码实现：

```c++
#include <iostream>
#include <string>
using namespace std;
#include <ctime>

int main()
{
    int scores[3][3] =
    {
        {100,100,100},
        {90,50,100},
        {60,70,80}
    };
    string name3[3] = { "张三","李四","王五" };
    int i = 0;
    int j = 0;
    int sum = 0;
    for (i = 0;i < 3;i++)
    {
        for (j = 0;j < 3;j++)
        {
            sum = sum + scores[i][j];
        }
        cout << name3[i] << "的总成绩为:" << sum << endl;
        sum = 0;
    }
    system("pause");
    return 0;
}
```

注意：

字符串也可以有数组

## 6 函数

### 6.1 概述

**作用：**将一段经常使用的代码封装起来，减少重复代码

一个较大的程序，一般分为若干个程序块，每个模块实现特定的功能。

### 6.2 函数的定义

函数的定义一般主要有5个步骤：

1、返回值类型 

2、函数名

3、参数表列

4、函数体语句 

5、return 表达式

**语法：** 

```C++
返回值类型 函数名 （参数列表）
{
       函数体语句
       return表达式
}
```

* 返回值类型 ：一个函数可以返回一个值。在函数定义中
* 函数名：给函数起个名称
* 参数列表：使用该函数时，传入的数据
* 函数体语句：花括号内的代码，函数内需要执行的语句
* return表达式： 和返回值类型挂钩，函数执行完后，返回相应的数据

**示例：**定义一个加法函数，实现两个数相加

```C++
//函数定义
int add(int num1, int num2)
{
	int sum = num1 + num2;
	return sum;
}
```

### 6.3 函数的调用

**功能：**使用定义好的函数

**语法：**` 函数名（参数）`

**示例：**

```C++
//函数定义
int add(int num1, int num2) //定义中的num1,num2称为形式参数，简称形参
{
	int sum = num1 + num2;
	return sum;
}

int main() {

	int a = 10;
	int b = 10;
	//调用add函数
	int sum = add(a, b);//调用时的a，b称为实际参数，简称实参
	cout << "sum = " << sum << endl;

	a = 100;
	b = 100;

	sum = add(a, b);
	cout << "sum = " << sum << endl;

	system("pause");

	return 0;
}
```

> 总结：函数定义里小括号内称为形参，函数调用时传入的参数称为实参

数组在函数中的调用一般形式：

```c++
void Array(int arr[],len)
{
    
}

或者是：
void Array(int *arr,len)
{
    
}
```

这两个都是指针的意思

### 6.4 值传递

* 所谓值传递，就是函数调用时实参将数值传入给形参
* 值传递时，==如果形参发生改变，并不会影响实参==



**示例：**

```C++
void swap(int num1, int num2)
{
	cout << "交换前：" << endl;
	cout << "num1 = " << num1 << endl;
	cout << "num2 = " << num2 << endl;

	int temp = num1;
	num1 = num2;
	num2 = temp;

	cout << "交换后：" << endl;
	cout << "num1 = " << num1 << endl;
	cout << "num2 = " << num2 << endl;

	//return ; 当函数声明时候，不需要返回值，可以不写return
}

int main() {

	int a = 10;
	int b = 20;

	swap(a, b);

	cout << "mian中的 a = " << a << endl;
	cout << "mian中的 b = " << b << endl;

	system("pause");

	return 0;
}
```

> 总结： 值传递时，形参是修饰不了实参的

==不返回值时，可以不写return，返回值类型是void==

### **6.5 函数的常见样式**

常见的函数样式有4种

1. 无参无返
2. 有参无返
3. 无参有返
4. 有参有返

### 6.6 函数的声明

**作用：** 告诉编译器函数名称及如何调用函数。函数的实际主体可以单独定义。



*  函数的**声明可以多次**，但是函数的**定义只能有一次**

**示例：**

```C++
//声明可以多次，定义只能一次
//声明
int max(int a, int b);	//这个是声明
int max(int a, int b);
//定义
int max(int a, int b)	//这个是定义
{
	return a > b ? a : b;
}

int main() {

	int a = 100;
	int b = 200;

	cout << max(a, b) << endl;

	system("pause");

	return 0;
}
```

==当函数在main（）函数后面时，一定要先声明==

### 6.7 函数的分文件编写

**作用：**让代码结构更加清晰

函数分文件编写一般有4个步骤

1. 创建后缀名为.h的头文件  
2. 创建后缀名为.cpp的源文件
3. 在头文件中写函数的声明
4. 在源文件中写函数的定义



1）.h头文件的创建：

右键头文件，新建项，以.h为后缀命名：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230223163714.png)

头文件代码：

```c++
//函数的声明
#include <iostream>
using namespace std;
void swap(int a, int b);	//声明函数要有分号
```

注意：==void声明函数后面要有分号==

   	==在声明前一定要加头文件==



2）.cpp源文件的创建：

右键源文件，创建新建项，以.cpp为后缀创建文件

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230223164053.png)

代码：

```c++
//函数的定义
#include "swap.h"
void swap(int a, int b)
{
	int temp = a;
	a = b;
	b = temp;
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
}
```

注意：==头文件要调用前面声明的.h文件==



3）主函数中的应用：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230223164237.png)

代码：

```c++
#include <iostream>
#include "swap.h"
using namespace std;

int main()
{
	int a = 10;
	int b = 20;
	swap(a, b);
	system("pause");
	return 0;
}
```

注意：==要在头文件中声明.h文件==

  	 ==在函数主题中直接使用函数即可，无需说明==





## 7 指针

### 7.1 指针的基本概念

**指针的作用：** 可以通过指针间接访问内存



* 内存编号是从0开始记录的，一般用十六进制数字表示

* 可以利用指针变量保存地址



1）在C++种创建指针时，计算机将分配==用来存储地址的内存==，但不会分配==用来存储指针所指向数据的内存==。

2）一定要在对指针应用解除引用运算符(*)之前，将==指针初始化为一个确定的、适当的地址==，这是使用指针的金科玉律。

3）要将数字值作为地址来使用，应通过强制类型转换将数字转换为适当的地址类型。

```c++
int* pt;
pt = (int *) 0XB8000000;
```

4）将指针变量加1后，其增加的值等于指向的类型占用的字节数。

5）对数组sizeof得到的是数组的长度，对指针sizeof得到的是指针的长度，即使指针指向的是一个数组



### 7.2 指针变量的定义和使用

指针变量定义语法： `数据类型 * 变量名；`

代码：

```c++
int main() {

	//1、指针的定义
	int a = 10; //定义整型变量a
	
	//指针定义语法： 数据类型 * 变量名 ;
	int * p;

	//指针变量赋值
	p = &a; //指针指向变量a的地址
	cout << &a << endl; //打印数据a的地址
	cout << p << endl;  //打印指针变量p

	//2、指针的使用
	//通过*操作指针变量指向的内存
	cout << "*p = " << *p << endl;

	system("pause");

	return 0;
}
```



指针变量和普通变量的区别：

==1）普通变量存放的是数据,指针变量存放的是地址==

==2）指针变量可以通过" * "操作符，操作指针变量指向的内存空间，这个过程称为解引用==

3）定义指针时，可以使用两种类型的定义：

```c++
int *p;
int* p;		//这种可以看作强调的是int*是一种类型，即指向int的指针。
int* p1,p2;		//这里定义的是指针p1和int变量p2.
```

4）指针变量不仅仅是指针，而且是指向特定类型的指针，和数组一样，指针都是基于其他类型的。

5）指针之间可以进行算数运算，仅当两个指针指向同一个数组时，这种运算才有意义

```c++
#include <iostream>
#include <string>
using namespace std;
#include <ctime>

int main()
{
    int tacos[10] = { 5,2,8,4,1,2,2,4,6,8 };
    int* pt = tacos;
    cout << "pt=" << pt << endl;
    pt = pt + 1;
    cout << "pt+1=" << pt << endl;

    int* pe = &tacos[9];
    cout << "pe=" << pe << endl;
    pe = pe - 1;
    cout << "pe-1=" << pe << endl;
    int diff = pe - pt;
    cout << "diff=" << diff << endl;
    system("pause");
    return 0;
}
```

![QQ图片20230315104533](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230315104533.png)



> 总结1： 我们可以通过 & 符号 获取变量的地址

> 总结2：利用指针可以记录地址

> 总结3：对指针变量解引用，可以操作指针指向的内存





### 7.3 指针所占内存空间



提问：指针也是种数据类型，那么这种数据类型占用多少内存空间？



**示例：**

```C++
int main() {

	int a = 10;

	int * p;
	p = &a; //指针指向数据a的地址

	cout << *p << endl; //* 解引用
	cout << sizeof(p) << endl;
	cout << sizeof(char *) << endl;
	cout << sizeof(float *) << endl;
	cout << sizeof(double *) << endl;
	//都是4
   	
	system("pause");

	return 0;
}
```



> 总结：所有指针类型在32位操作系统下是4个字节，64位下是8个字节

### 7.4 空指针和野指针

**空指针**：指针变量指向内存中编号为0的空间

**用途：**初始化指针变量

**注意：**空指针指向的内存是不可以访问的



**示例1：空指针**

```C++
int main() {

	//指针变量p指向内存地址编号为0的空间
	int * p = NULL;

	//访问空指针报错 
	//内存编号0 ~255为系统占用内存，不允许用户访问
	cout << *p << endl;

	system("pause");

	return 0;
}
```

**野指针**：指针变量指向非法的内存空间



**示例2：野指针**

```C++
int main() {

	//指针变量p指向内存地址编号为0x1100的空间
	int * p = (int *)0x1100;

	//访问野指针报错 
	cout << *p << endl;

	system("pause");

	return 0;
}
```

> 总结：空指针和野指针都不是我们申请的空间，因此不要访问。

### 7.5 const修饰指针

const修饰指针有三种情况

1. const修饰指针   --- 常量指针
2. const修饰常量   --- 指针常量
3. const即修饰指针，又修饰常量




**示例：**


```c++
int main() {

	int a = 10;
	int b = 10;

	//const修饰的是指针，指针指向可以改，指针指向的值不可以更改,常量指针
	const int * p1 = &a; 
	p1 = &b; //正确
	//*p1 = 100;  报错
	

	//const修饰的是常量，指针指向不可以改，指针指向的值可以更改，指针常量
	int * const p2 = &a;
	//p2 = &b; //错误
	*p2 = 100; //正确

    //const既修饰指针又修饰常量
	const int * const p3 = &a;
	//p3 = &b; //错误
	//*p3 = 100; //错误

	system("pause");

	return 0;
}
```



> 技巧：看const右侧紧跟着的是指针还是常量, 是指针就是常量指针，是常量就是指针常量

可以理解为const修饰的是*p还是p

第一种情况相当于const修饰的是*p，所以 *p不可以改，但是p可以改，称为常量指针。

第二种情况相当于const修饰的是p，所以p不可以改，但是*p可以改，称为指针常量。

### 7.6 指针和数组

**作用：**利用指针访问数组中元素

代码：

```c++
#include <iostream>
#include "swap.h"
using namespace std;

int main() 
{	
	int arr[] = { 1,2,3,4,5,6,7,8,9,10 };
	int* p = arr;
	int i = 0;
	for (i = 0 ; i < 10 ; i++)
	{
		cout << *p << endl;
		p++;
	}
	system("pause");
	return 0;
}
```

注意：==指针p++可以直接代表下一个变量的地址==

### 7.7 指针和函数

**作用：**利用指针作函数参数，可以修改实参的值



**示例：**

```C++
//值传递
void swap1(int a ,int b)
{
	int temp = a;
	a = b; 
	b = temp;
}
//地址传递
void swap2(int * p1, int *p2)
{
	int temp = *p1;
	*p1 = *p2;
	*p2 = temp;
}
int main()
{
	int a = 10;	//这是实参
	int b = 20;
	swap1(a, b); // 值传递不会改变实参
	swap2(&a, &b); //地址传递会改变实参
	cout << "a = " << a << endl;
	cout << "b = " << b << endl;
	system("pause");
	return 0;
}
```



> 总结：如果不想修改实参，就用值传递，如果想修改实参，就用地址传递



### 7.8 指针、数组、函数

**案例描述：**封装一个函数，利用冒泡排序，实现对整型数组的升序排序

例如数组：int arr[10] = { 4,3,6,9,1,2,10,8,7,5 };

```c++
#include <iostream>
#include "swap.h"
using namespace std;

//冒泡排序函数:
void bubblesort(int* arr, int len)
{
	int temp = 0;
	for (int i = 0;i < len - 1;i++)
	{
		for (int j = 0;j < len - i - 1;j++)
		{
			if (arr[j] > arr[j + 1])
			{
				temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	}
}

//输出排序后的函数
void printarray(int* arr, int len)
{
	int i = 0;
	for (i = 0;i < len;i++)
	{
		cout << arr[i] << endl;
	}
}

//主函数
int main() 
{	
	int arr[10] = { 4,3,6,9,1,2,10,8,7,5 };
	int len = sizeof(arr) / sizeof(arr[0]);
	bubblesort(arr, len);
	printarray(arr, len);
	system("pause");
	return 0;
}
```

注意：==若想向函数传递数组，则需要在函数变量中定义指针，在函数中直接调用数组即可==

## 8 结构体

### 8.1 结构体基本概念

结构体属于用户==自定义的数据类型==，允许用户存储不同的数据类型



### 8.2 结构体定义和使用

**语法：**`struct 结构体名 { 结构体成员列表 }；`

通过结构体创建变量的方式有三种：

* struct 结构体名 变量名
* struct 结构体名 变量名 = { 成员1值 ， 成员2值...}
* 定义结构体时顺便创建变量

示例：

```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};

int main() 
{	
	student s1;
	s1.name = "李华";
	s1.age = 22;
	s1.score = 100;
	cout << "姓名：" <<  s1.name  << " 年纪：" <<  s1.age  << " 分数 : " <<  s1.score << endl;
	student s2 = { "小明", 23 , 90 };
	cout << "姓名：" << s2.name << " 年纪：" << s2.age << " 分数 : " << s2.score << endl;
	system("pause");
	return 0;
}
```

注意：一般是用前两种方式来定义结构体数据

定义结构体时，要加分号，不可省去struct；创建结构体变量时，可以省去struct。

### 8.3 结构体数组

**作用：**将自定义的结构体放入到数组中方便维护

**语法：**` struct  结构体名 数组名[元素个数] = {  {} , {} , ... {} }`



示例：

```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};

int main() 
{	
	struct student stuArray[3] =
	{
		{"李华",18,100},
		{"李四",18,98},
		{"小明",19,99}
	};
	stuArray[2].name = "赵四";
	stuArray[2].age = 90;
	stuArray[2].score = 60;

	for (int i = 0;i < 3;i++)
	{
		cout << "姓名: " << stuArray[i].name << " 年龄: " << stuArray[i].age << " 分数: " << stuArray[i].score << endl;
	}
	system("pause");
	return 0;
}
```



注意：==1）结构体数组使用时用的是数组名==。

​			2）如果大括号内没有任何东西，则各个成员都将被设置为0。

### 8.4 结构体指针

**作用：**通过指针访问结构体中的成员



* 利用操作符 `-> `可以通过结构体指针访问结构体属性



```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};

int main() 
{	
	struct student s1 = { "张三",20,90 };
	struct student* p = &s1;
	p->score = 100;
	cout << "姓名： " << p->name << "年龄： " << p->age << "成绩： " << p->score << endl;
	system("pause");
	return 0;
}
```

注意：1.用指针访问结构体时，访问的时结构体的地址

​			2.可以通过p-> = 来改变结构体中的数据





### 8.5 结构体嵌套结构体

**作用：** 结构体中的成员可以是另一个结构体

**例如：**每个老师辅导一个学员，一个老师的结构体中，记录一个学生的结构体

示例：

```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};

struct teacher
{
	string name;
	int id;
	int age;
	struct student s1;
};

int main() 
{	
	struct teacher t1 = { "李华",2022,43,{"小明",20,100} };

	cout << " 老师姓名： " << t1.name << " 老师年纪： " << t1.age << " 老师学号： " << t1.id << endl;
	cout << " 学生名字： " << t1.s1.name << " 学生年龄： " << t1.s1.age << " 学生成绩 " << t1.s1.score << endl;
	system("pause");
	return 0;
}
```

当然也可以使用以下语句来给结构体变量赋值：

```c++
struct teacher t1;
	t1.id = 10000;
	t1.name = "老王";
	t1.age = 40;

	t1.stu.name = "张三";
	t1.stu.age = 18;
	t1.stu.score = 100;
```



注意：1.teacher结构体必须定义在student结构体下面

​			2.结构体中的结构体可以通过t1.s1.name这种形式来调用



### 8.6 结构体做函数参数 

**作用：**将结构体作为参数向函数中传递

传递方式有两种：

* 值传递
* 地址传递

```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};


//值传递
void printStudent1(struct student s1)
{
	s1.age = 80;
	cout << " student1 print : " << s1.name << " age : " << s1.age << " score " << s1.score << endl;
}


//地址传递
void printStudent2(struct student* p)
{
	p->age = 60;
	cout << " student2 print : " << p->name << " age : " << p->age << " score " << p->score << endl;
}


int main() 
{	
	struct student s1 = { "王策",23,100 };
	cout << " main print : " << s1.name << " age : " << s1.age << " score " << s1.score << endl;

	printStudent1(s1);
	printStudent2(&s1);

	cout << " main2 print : " << s1.name << " age : " << s1.age << " score " << s1.score << endl;
	system("pause");
	return 0;
}
```



注意：1.地址传递会改变main函数中的数值，值传递并不会改变main函数中的数值。

​			2.调用函数时，==地址使用的是结构体的地址&s1，值用的是结构体s1。==

​			3.在函数中使用地址时，调用结构体用的是p->，而值传递时用的是s1.name。

### 8.7 结构体中 const使用场景

**作用：**用const来防止误操作

示例：

```c++
#include <iostream>
#include "swap.h"
#include <string>
using namespace std;

struct student
{
	string name;
	int age = 0;
	int score = 0;
};

//const使用场景
void printStudent(const student* p)
{
	//p->age = 60; 系统提示不可修改
	cout << " student print : " << p->name << " age : " << p->age << " score " << p->score << endl;
}

int main() 
{	
	struct student s1 = { "王策",23,100 };
	cout << " main print : " << s1.name << " age : " << s1.age << " score " << s1.score << endl;
	printStudent(&s1);
	system("pause");
	return 0;
}
```

注意：1.用地址传递而不是值传递的原因是，这样会提高运行效率

​	   2.地址传递前有const后，在函数中就不再可以修改结构体内容



### 8.8 结构体案例

#### 8.8.1 案例1

**案例描述：**

学校正在做毕设项目，每名老师带领5个学生，总共有3名老师，需求如下

设计学生和老师的结构体，其中在老师的结构体中，有老师姓名和一个存放5名学生的数组作为成员

学生的成员有姓名、考试分数，创建数组存放3名老师，通过函数给每个老师及所带的学生赋值

最终打印出老师数据以及老师所带的学生数据。

```c++
#include <iostream>
#include <ctime>
#include <string>

using namespace std;

//定义学生结构体
struct student
{
	string name;
	int score = 0;
};

//定义老师结构体
struct teacher
{
	string name;
	student sArray[5];
};

//老师和学生的分配函数
void allocateArray(teacher tArray[],int len)
{
	string name = "ABCDE";
	for (int i = 0;i < len;i++)
	{
		tArray[i].name = "老师_";
		tArray[i].name += name[i];
		for (int j = 0;j < 5;j++)
		{
			tArray[i].sArray[j].name = "学生_";
			tArray[i].sArray[j].name += name[j];
			int random = rand() % 61 + 40;	//随机数函数
			tArray[i].sArray[j].score = random;
		}
	}
}

void printfArray(teacher tArray[], int len)
{
	for (int i = 0;i < len;i++)
	{
		cout << tArray[i].name<< endl;
		for (int j = 0;j < 5;j++)
		{
			cout << "\t姓名：" << tArray[i].sArray[j].name << " 分数： " << tArray[i].sArray[j].score << endl;
		}
	}
}

int main() 
{	
	//随机数时间初始化函数:
	srand((unsigned int)time(NULL));
	//老师结构体数组
	struct teacher tArray[3];
	int len = sizeof(tArray) / sizeof(tArray[0]);
	allocateArray(tArray,len);	//给的是结构体数组名
	printfArray(tArray, len);
	system("pause");
	return 0;
}
```



注意：1.结构体数组调用函数时，输入的是数组名，即指针。

​			2.函数定义时，若想调用结构体数组，则定义的是(teacher arr[])。

​			3.结构体数组到函数中后，直接视作数组使用即可。



#### 8.8.2 案例2

**案例描述：**

设计一个英雄的结构体，包括成员姓名，年龄，性别;创建结构体数组，数组中存放5名英雄。

通过冒泡排序的算法，将数组中的英雄按照年龄进行升序排序，最终打印排序后的结果。

五名英雄信息如下：

```C++
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"},
```

示例：

```c++
#include <iostream>
#include <string>
using namespace std;

struct hero
{
	string name;
	int age;
	string sex;
};

//冒泡排序
void bubblesort(hero array[], int len)
{
	for (int i = 0;i < len;i++)
	{
		for (int j = 0;j < len - i - 1;j++)
		{
			if (array[j].age > array[j + 1].age)
			{
				/*int temp = array[j].age;
				array[j].age = array[j + 1].age;
				array[j + 1].age = temp;

				string temp1 = array[j].name;
				array[j].name = array[j + 1].name;
				array[j + 1].name = temp1;

				string temp2 = array[j].sex;
				array[j].sex = array[j + 1].sex;
				array[j + 1].sex = temp2;*/
				//上面这种替换太繁琐了，最好用下面这个
               
				hero temp = array[j];
				array[j] = array[j + 1];
				array[j + 1] = temp;
			}
		}
	}
}

//输出函数
void printfArray(hero array[], int len)
{
	for (int i = 0 ;i < len;i++)
	{
		cout << array[i].age << array[i].name << array[i].sex << endl;
	}
}

int main()
{
	hero array[5] =
	{
		{"刘备",23,"男"},
		{"关羽",22,"男"},
		{"张飞",20,"男"},
		{"赵云",21,"男"},
		{"貂蝉",19,"女"},
	};
	int len = sizeof(array) / sizeof(array[0]);
	bubblesort(array,len);
	printfArray(array, len);
	system("pause");
	return 0;
}
```



注意：1.冒泡排序结构体数组时，可以直接用结构体命名temp，来进行结构体数据的替换。



# 二.C++核心编程



## 1.内存分区模型



### 1.1 程序运行前：

- 代码区：只读和共享


- 全局区：全局变量，静态变量，字符串常量，全局常量


![BF38DD9FF0AC530E9BF1FD6AB1BDB9C5](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/BF38DD9FF0AC530E9BF1FD6AB1BDB9C5.png)

### 1.2 程序运行后：

栈区：存放函数的参数值、局部变量等，不要返回局部变量的地址，栈区开辟的数据由编译器自动释放

堆区：由程序员分配释放，若程序员不释放，程序结束时操作系统回收，在C++中主要利用new在堆区开辟内存

### 1.3 new操作符

C++中利用new操作符在堆区开辟数据

堆区开辟的数据，由程序员手动开辟，手动释放，释放利用操作符delete，具体代码见讲义，利用new创建的数据，会返回该数据对应的类型的指针，删除数组时，delete后应加[]操作符

## 2.引用

### 2.1 引用的基本使用

**作用： **给变量起别名

**语法：** `数据类型 &别名 = 原名`

### 2.2 引用注意事项

* 引用必须初始化
* 引用在初始化后，不可以改变

### 2.3 引用做函数参数

**作用：**函数传参时，可以利用引用的技术让形参修饰实参

**优点：**可以简化指针修改实参

### 2.4 引用做函数返回值

作用：引用是可以作为函数的返回值存在的

注意：**不要返回局部变量引用**，如果想返回函数中的引用，最好加上static把变量变为全局变量

用法：函数调用作为左值

### 2.5 引用的本质

本质：**引用的本质在c++内部实现是一个指针常量.**

### 2.6 常量引用

**作用：**常量引用主要用来修饰形参，防止误操作

在函数形参列表中，可以加==const修饰形参==，防止形参改变实参

## 3.函数提高



### 3.1函数默认参数

在C++中，函数的形参列表中的形参是可以有默认值的。

语法：` 返回值类型  函数名 （参数= 默认值）{}`

1. 如果某个位置参数有默认值，那么从这个位置往后，从左向右，必须都要有默认值
2. 如果函数声明有默认值，函数实现的时候就不能有默认参数，即函数声明和函数默认二者之间只能有一个地方有函数默认参数

### 3.2函数占位参数



C++中函数的形参列表里可以有占位参数，用来做占位，调用函数时必须填补该位置

**语法：** `返回值类型 函数名 (数据类型){}`

函数占位参数 ，占位参数也可以有默认参数

```c++
void func(int a, int)
//或者是:
void func(int a,int=10)
    
int main()
{
    func(1,1);
}
```



### 3.3函数重载



**作用：**函数名可以相同，提高复用性

**函数重载满足条件：**

* 同一个作用域下
* 函数名称相同
* 函数参数**类型不同**  或者 **个数不同** 或者 **顺序不同**

**注意:**  函数的返回值不可以作为函数重载的条件

注意事项请看讲义，引用和函数默认参数

引用时若有无const会决定调用函数的不同

函数默认参数在定义不同函数时要尽量避免重载，因为那样会产生歧义



### 3.4Lambda表达式

基本语法：

```c++
[捕获列表](参数列表) -> 返回值类型 {
    函数体
};
```

**捕获列表 `[ ]`**：

- 用于指定 Lambda 表达式可以访问的外部作用域中的变量。
- 可选择捕获方式（值捕获[=]、引用捕获[&]等）。

**参数列表 `( )`**：

- 类似普通函数的参数列表，用于传递参数。
- 如果没有参数，可以省略括号。

**返回值类型 `-> 返回值类型`**（可选）：

- 明确指定返回值类型。如果可以自动推断，则可以省略。

**函数体 `{ }`**：

- Lambda 表达式的核心逻辑。

参考链接：

https://blog.csdn.net/m0_60134435/article/details/136151698

## 4.类和对象



### 4.1封装

**语法：** `class 类名{   访问权限： 属性  / 行为  };`

类在设计时，可以把属性和行为放在不同的权限下，加以控制

访问权限有三种：

1. public        公共权限  
2. protected 保护权限
3. private      私有权限

```c++
//三种权限
//公共权限  public     类内可以访问  类外可以访问
//保护权限  protected  类内可以访问  类外不可以访问
//私有权限  private    类内可以访问  类外不可以访问
```

在C++中 struct和class唯一的**区别**就在于 **默认的访问权限不同**

区别：

* struct 默认权限为公共
* class   默认权限为私有

设计一个立方体类

求出立方体的面积和体积

分别用全局函数和成员函数判断两个立方体是否相等。

```c++
#include <iostream>
#include <string>

using namespace std;

class Cube
{

	//设置成员属性：
private:
	//定义长宽高
	int m_L;
	int m_W;
	int m_H;

	//设置成员行为：
public:
	//获取长宽高：
	void setL(int L)
	{
		m_L = L;
	}
	void setW(int W)
	{
		m_W = W;
	}
	void setH(int H)
	{
		m_H = H;
	}

	//展示长宽高：
	int showL()
	{
		return m_L;
	}
	int showW()
	{
		return m_W;
	}
	int showH()
	{
		return m_H;
	}

	//获取立方体面积：
	int caculateS()
	{
		return 2 * m_L * m_W + 2 * m_L * m_H + 2 * m_W * m_H;
	}
	//获取立方体体积
	int caculateV()
	{
		return m_L * m_H * m_W;
	}
	//通过成员函数判断两个立方体是否相等
	bool IsName(Cube &C)
	{
		if (m_L == C.showL() && m_W == C.showW() && m_H == C.showH())
		{
			return true;
		}
		else
		{
			return false;
		}
	}
};


//全局函数判断两个立方体是否相等：
bool IsSame(Cube& C1, Cube& C2)
{
	if (C1.showL() == C2.showL() && C1.showW() == C2.showW() && C1.showH() == C2.showH())
	{
		return true;
	}
	else
	{
		return false;
	}
}

int main()
{
	Cube C1;
	Cube C2;
	C1.setL(10);
	C1.setH(10);
	C1.setW(10);

	C2.setL(10);
	C2.setH(10);
	C2.setW(10);

	cout << "面积是：" << C1.caculateS() << endl;
	cout << "体积是：" << C1.caculateV() << endl;

	//全局函数判断两立方体是否相等
	bool ret1 = IsSame(C1, C2);
	if (ret1)
	{
		cout << "通过全局函数可知两立方体相等" << endl;
	}
	else
	{
		cout << "通过全局函数可知两立方体不相等" << endl;
	}

	//内部函数判断两立方体是否相等
	bool ret2 = C1.IsName(C2);
	if (ret2)
	{
		cout << "通过成员函数可知两立方体相等" << endl;
	}
	else
	{
		cout << "通过成员函数可知两立方体不相等" << endl;
	}
	system("pause");
	return 0;
}
```

设计一个圆形类（Circle），和一个点类（Point），计算点和圆的关系。

```c++
#include <iostream>
#include <string>

using namespace std;

//设计圆类
class Circle
{
	//成员属性设置圆的半径，x和y轴坐标
private:
	int c_r;
	int c_x;
	int c_y;

	//成员行为设置获取半径，x和y轴坐标以及输出对应的值
public:
	//获取半径、x和y轴坐标的值
	void getr(int r)
	{
		c_r = r;
	}
	void getx(int x)
	{
		c_x = x;
	}
	void gety(int y)
	{
		c_y = y;
	}
	//输出半径、x和y轴坐标的值
	int showr()
	{
		return c_r;
	}
	int showx()
	{
		return c_x;
	}
	int showy()
	{
		return c_y;
	}

};

//设计点类
class Point
{
	//成员属性设置点的x和y轴坐标
private:
	int p_x;
	int p_y;

	//成员行为设置获取x和y轴坐标的值以及输出对应的值
public:
	//获取x和y轴坐标的值
	void getx(int x)
	{
		p_x = x;
	}
	void gety(int y)
	{
		p_y = y;
	}
	//输出x和y轴坐标的值
	int showx()
	{
		return p_x;
	}
	int showy()
	{
		return p_y;
	}
};

//设计一个判断点和圆关系的函数
//系统传入两个类引用，而后通过引用的数据计算距离和半径之间的关系
//如果点在圆内返回1，点在园外返回2，点在圆上返回3.

int distanceCAP(Circle& c, Point& p)
{
	//首先计算点和圆心之间的距离的平方：
	int distance = (c.showx() - p.showx()) * (c.showx() - p.showx()) + (c.showy() - p.showy()) * (c.showy() - p.showy());
	//表示圆半径的平方：
	int r2 = c.showr() * c.showr();

	//如果r2>distance，点在园内返回1
	//如果r2<distance，点在园外返回2
	//如果r2=distance，点在圆上返回3
	if (r2 > distance)
	{
		return 1;
	}
	else if (r2 < distance)
	{
		return 2;
	}
	else
	{
		return 3;
	}
}

int main()
{
	//设计圆类和点类
	Circle C;
	Point P;
	int select = 1;
	while (select)
	{
		int cr = 0;
		int cx = 0;
		int cy = 0;
		int px = 0;
		int py = 0;

		//给出圆的坐标和半径
		cout << "请输入圆的半径：" << endl;
		cin >> cr;
		cout << "请输入圆的x轴坐标：" << endl;
		cin >> cx;
		cout << "请输入圆的y轴坐标：" << endl;
		cin >> cy;
		C.getr(cr);
		C.getx(cx);
		C.gety(cy);

		//给出点的坐标和半径
		cout << "请输入点的x轴坐标：" << endl;
		cin >> px;
		cout << "请输入点的y轴坐标：" << endl;
		cin >> py;
		P.getx(px);
		P.gety(py);
		//判断二者之间的关系
		int d = distanceCAP(C, P);
		if (d == 1)
		{
			cout << "点在圆内" << endl;
		}
		else if (d == 2)
		{
			cout << "点在圆外" << endl;
		}
		else
		{
			cout << "点在圆上" << endl;
		}

		//判断是否要继续循环：
		cout << "您若还想继续判断点与圆的关系请输入1，想退出请输入0" << endl;
		cin >> select;
		system("cls");
	}
	
	system("pause");
	return 0;
}
```

或由于圆心也是个点类，所以可以在圆类内包含点类，即类包含类，具体如下

```c++
#include <iostream>
#include <string>
#include "point.h"
#include "circle.h"


using namespace std;

//设计点类
class Point
{
	//成员属性设置点的x和y轴坐标
private:
	int p_x;
	int p_y;

	//成员行为设置获取x和y轴坐标的值以及输出对应的值
public:
	//获取x和y轴坐标的值
	void getx(int x)
	{
		p_x = x;
	}
	void gety(int y)
	{
		p_y = y;
	}
	//输出x和y轴坐标的值
	int showx()
	{
		return p_x;
	}
	int showy()
	{
		return p_y;
	}
};

//设计圆类
class Circle
{
	//成员属性设置圆的半径，x和y轴坐标
private:
	int c_r;
	Point c_Center;

	//成员行为设置获取半径，x和y轴坐标以及输出对应的值
public:
	//获取半径值
	void getr(int r)
	{
		c_r = r;
	}
	//输出半径值
	int showr()
	{
		return c_r;
	}
	//获取圆心的值：
	void getCenter(Point C)
	{
		c_Center = C;
	}
	//输出圆心的值：
	Point showCenter()
	{
		return c_Center;
	}
};

//判断点和圆关系的函数
void DistancePAC(Circle& C, Point& P)
{
	int distance =
		(C.showCenter().showx() - P.showx()) * (C.showCenter().showx() - P.showx()) +
		(C.showCenter().showy() - P.showy()) * (C.showCenter().showy() - P.showy());
	int r2 = C.showr() * C.showr();
	if (distance > r2)
	{
		cout << "外" << endl;
	}
	else if (distance < r2)
	{
		cout << "内" << endl;
	}
	else
	{
		cout << "上" << endl;
	}
}


int main()
{
	Point P;
	Circle C;
	//设置点的坐标
	P.getx(0);
	P.gety(0.5);
	//设置圆的坐标
	C.getr(1);
	Point Center;
	Center.getx(0);
	Center.gety(0);
	C.getCenter(Center);
	DistancePAC(C, P);
	system("pause");
	return 0;
}
```

由于在主函数体内设计类太乱，所以可以对类进行封装，具体如下：

点类的.h文件如下：

```c++
#pragma once
#include <iostream>
using namespace std;
//设计点类
class Point
{
	//成员属性设置点的x和y轴坐标
private:
	int p_x;
	int p_y;
	//成员行为设置获取x和y轴坐标的值以及输出对应的值
public:
	//获取x和y轴坐标的值
	void getx(int x);
	void gety(int y);
	//输出x和y轴坐标的值
	int showx();
	int showy();
};
```

点类的.cpp文件如下：

```c++
#include "point.h"


void Point::getx(int x)
{
	p_x = x;
}
void Point::gety(int y)
{
	p_y = y;
}
//输出x和y轴坐标的值
int Point::showx()
{
	return p_x;
}
int Point::showy()
{
	return p_y;
}
```

圆类的.h文件如下：

```c++
#pragma once
#include <iostream>
using namespace std;
#include "point.h"
//设计圆类
class Circle
{
	//成员属性设置圆的半径，x和y轴坐标
private:
	int c_r;
	Point c_Center;

	//成员行为设置获取半径，x和y轴坐标以及输出对应的值
public:
	//获取半径值
	void getr(int r);
	int showr();
	void getCenter(Point C);
	Point showCenter();
};
```

圆类的.cpp文件如下：

```c++
#include "circle.h"

//获取半径值
void Circle::getr(int r)
{
	c_r = r;
}
//输出半径值
int Circle::showr()
{
	return c_r;
}
//获取圆心的值：
void Circle::getCenter(Point C)
{
	c_Center = C;
}
//输出圆心的值：
Point Circle::showCenter()
{
	return c_Center;
}
```

具体规律：

1..h文件内的类需要进行声明，但是对于函数的具体操作不需要进行处理

2..cpp文件内不需要进行类和函数的声明，但是对于函数的具体操作要进行标注处理

3.cpp文件内函数前要加上对应的类的对应域，即Circle::这种字眼

有不懂的可以打开20240122文件的封装来看看

### 4.2对象的初始化和清理

#### 4.2.1构造函数和析构函数



* 构造函数：主要作用在于创建对象时为对象的成员属性赋值，构造函数由编译器自动调用，无须手动调用。
* 析构函数：主要作用在于对象**销毁前**系统自动调用，执行一些清理工作。



**构造函数语法：**`类名(){}`

1. 构造函数，没有返回值也不写void
2. 函数名称与类名相同
3. 构造函数可以有参数，因此可以发生重载
4. 程序在调用对象时候会自动调用构造，无须手动调用,而且只会调用一次





**析构函数语法：** `~类名(){}`

1. 析构函数，没有返回值也不写void
2. 函数名称与类名相同,在名称前加上符号  ~
3. 析构函数不可以有参数，因此不可以发生重载
4. 程序在对象销毁前会自动调用析构，无须手动调用,而且只会调用一次



#### 4.2.2构造函数的分类及调用

两种分类方式：

​	按参数分为： 有参构造和无参构造

​	按类型分为： 普通构造和拷贝构造

三种调用方式：

​	括号法

​	显示法

​	隐式转换法



```c++
class Person
{
public:
	//无参构造函数
	Person()
	{
		cout << "无参构造函数的调用" << endl;
	}
	//有参构造函数
	Person(int a)
	{
		cout << "有参构造函数的调用" << endl;
	}
	//拷贝构造函数
	Person(const Person& p)
	{
		m_age = p.m_age;
		cout << "拷贝构造函数的调用" << endl;
	}
    //析构函数
	~Person()
	{
		cout << "析构函数的调用" << endl;
	}
public:
	int m_age = 0;     
}
```

调用方式：

```c++
//无参构造函数的调用
void test01()
{
	Person p;
}

//有参构造函数的调用
void test02()
{
	Person p1(10);			//括号法
	Person p2 = Person(10);	//显式法
	Person p3 = 10;			//隐式转换法
}

//拷贝构造函数的调用
void test03()
{
	Person p = 10;
	Person p1(p);
	Person p2 = Person(p1);
	Person p3 = p2;
}
```



#### 4.2.3拷贝构造函数调用时机



C++中拷贝构造函数调用时机通常有三种情况

* 使用一个已经创建完毕的对象来初始化一个新对象
* 值传递的方式给函数参数传值
* 以值方式返回局部对象





#### 4.2.4构造函数的调用规则

默认情况下，c++编译器至少给一个类添加3个函数

1．默认构造函数(无参，函数体为空)

2．默认析构函数(无参，函数体为空)

3．默认拷贝构造函数，对属性进行值拷贝



构造函数调用规则如下：

* 如果用户定义有参构造函数，c++不在提供默认无参构造，但是会提供默认拷贝构造


* 如果用户定义拷贝构造函数，c++不会再提供其他构造函数



#### 4.2.5深拷贝与浅拷贝

深浅拷贝是面试经典问题，也是常见的一个坑

浅拷贝：简单的赋值拷贝操作

深拷贝：在堆区重新申请空间，进行拷贝操作

在堆区开辟数据时，如果要析构，那么要用深拷贝，即拷贝构造函数，否则浅拷贝会造成同一地址区域数据两次释放，具体操作可看代码，这里没咋学明白



#### 4.2.6初始化列表

**作用：**

C++提供了初始化列表语法，用来初始化属性

**语法：**`构造函数()：属性1(值1),属性2（值2）... {}`



```c++
class Person
{
public:
	//初始化列表：
	Person(int a, int b, int c) :m_a(a), m_b(b), m_c(c)
	{
		cout << "有参构造函数调用" << endl;
	}
	~Person()
	{
		cout << "析构函数调用" << endl;
	}
	void PrintPerson()
	{
		cout << "a=" << m_a << "b=" << m_b << "c=" << m_c << endl;
	}
private:
	int m_a;
	int m_b;
	int m_c;
};
```



#### 4.2.7类对象作为类成员



C++类中的成员可以是另一个类的对象，我们称该成员为 对象成员

例如：

```C++
class A {}
class B
{
    A a；
}
//当类中成员是其他类对象时，我们称该成员为 对象成员
//构造的顺序是 ：先调用对象成员的构造，再调用本类构造
//析构顺序与构造相反,先进后出
```

B类中有对象A作为成员，A为对象成员



#### 4.2.8静态成员



静态成员就是在成员变量和成员函数前加上关键字static，称为静态成员

静态成员分为：

*  静态成员变量
   *  所有对象共享同一份数据
   *  在编译阶段分配内存
   *  类内声明，类外初始化
*  静态成员函数
   *  所有对象共享同一个函数
   *  静态成员函数只能访问静态成员变量



1.静态成员变量：

```c++
class Person
{
public:
	static int m_A; //静态成员变量
	//静态成员变量特点：
	//1 在编译阶段分配内存
	//2 类内声明，类外初始化
	//3 所有对象共享同一份数据
private:
	static int m_B; //静态成员变量也是有访问权限的
};
int Person::m_A = 10;
int Person::m_B = 10;

void test01()
{
	//静态成员变量两种访问方式
	//1、通过对象
	Person p1;
	p1.m_A = 100;
	cout << "p1.m_A = " << p1.m_A << endl;
	Person p2;
	p2.m_A = 200;
	cout << "p1.m_A = " << p1.m_A << endl; //共享同一份数据
	cout << "p2.m_A = " << p2.m_A << endl;
	//2、通过类名
	cout << "m_A = " << Person::m_A << endl;
	//cout << "m_B = " << Person::m_B << endl; //私有权限访问不到
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

2.静态成员函数：

```c++
class Person
{
public:
	//静态成员函数特点：
	//1 程序共享一个函数
	//2 静态成员函数只能访问静态成员变量
	static void func()
	{
		cout << "func调用" << endl;
		m_A = 100;
		//m_B = 100; //错误，不可以访问非静态成员变量
	}
	static int m_A; //静态成员变量
	int m_B; // 
private:
	//静态成员函数也是有访问权限的
	static void func2()
	{
		cout << "func2调用" << endl;
	}
};
int Person::m_A = 10;

void test01()
{
	//静态成员变量两种访问方式
	//1、通过对象
	Person p1;
	p1.func();
	//2、通过类名
	Person::func();
    
	//Person::func2(); //私有权限访问不到
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```



### 4.3C++对象模型和this指针

#### 4.3.1成员变量和成员函数分开存储

在C++中，类内的成员变量和成员函数分开存储

只有非静态成员变量才属于类的对象上



1.空对象

```c++
#include <iostream>
using namespace std;
class Person
{

};

void test01()
{
	Person p;
	cout << sizeof(p) << endl;	
    //空对象占用内存空间为：1
    //C++编译器会给每个空对象分配一个字节空间，为了区分空对象占内存的位置
    //每个空对象也应该有一个独一无二的内存地址
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

2.非静态成员变量：

```c++
#include <iostream>
using namespace std;
class Person
{
	int a;	//非静态成员变量 属于类的对象上
    static int m_b;	//静态成员变量 不属于类对象上
    void func1()		//非静态成员函数 不属于类对象上
    static void func2()	//静态成员函数 不属于类的对象上
};

void test01()
{
	Person p;
	cout << sizeof(p) << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.3.2this指针



c++通过提供特殊的对象指针，this指针，解决上述问题。**this指针指向被调用的成员函数所属的对象**

this指针是隐含每一个非静态成员函数内的一种指针，this指针不需要定义，直接使用即可

this指针的用途：

*  当形参和成员变量同名时，可用this指针来区分
*  在类的非静态成员函数中返回对象本身，可使用return *this



1.当形参和成员变量同名时：

```c++
#include <iostream>

using namespace std;

class Person
{
public:
	Person(int age)
	{
		this->age = age;
	}
public:
	int age;
};

void test01()
{
	Person p1(10);
	cout << "p1的年龄为：" << p1.age << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

但是仍然建议使用不同名称来命名，防止这种错误

2.返回对象本身时：

```c++
#include <iostream>

using namespace std;

class Person
{
public:
	Person(int age)
	{
		this->age = age;
	}

	Person& PersonAdd(Person &p)
	{
		this->age += p.age;
		return *this;
	}

public:
	int age;
};

void test01()
{
	Person p1(10);
	cout << "p1的年龄为：" << p1.age << endl;
	Person p2(10);
	p2.PersonAdd(p1).PersonAdd(p1).PersonAdd(p1);
	cout << "p2的年龄为：" << p2.age << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

1.返回的是*this，this是一个指向p2的指针，所以 * this就是p2本身

2.返回的要是p2本身的引用，如果不是返回的引用，那么最后也不能构成年龄不断相加的这个结果。



#### 4.3.3空指针访问成员函数

C++中空指针也是可以调用成员函数的，但是也要注意有没有用到this指针

如果用到this指针，需要加以判断保证代码的健壮性



```c++
//空指针访问成员函数
class Person {
public:

	void ShowClassName() {
		cout << "我是Person类!" << endl;
	}
	void ShowPerson() {
		if (this == NULL) {
			return;
		}
		cout << mAge << endl;
	}

public:
	int mAge;
};

void test01()
{
	Person * p = NULL;
	p->ShowClassName(); //空指针，可以调用成员函数
	p->ShowPerson();  //但是如果成员函数中用到了this指针，就不可以了
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

如果没有if语句，程序会报错，因为this这时是空指针，无法只想age的数据



#### 4.3.4const修饰成员函数

**常函数：**

* 成员函数后加const后我们称为这个函数为**常函数**
* 常函数内不可以修改成员属性
* 成员属性声明时加关键字mutable后，在常函数中依然可以修改

**常对象：**

* 声明对象前加const称该对象为常对象
* 常对象只能调用常函数



常函数：

```c++
#include <iostream>

using namespace std;

class Person
{
public:

	void showPerson()const
	{
        this=NULL;	//报错
		m_a = 10;	//报错
        //此时会报错，因为this指针的本质 是指针常量 指针的指向是不可以修改的
        //在成员函数后面加const，修饰的是this指向，让指针指向的值也不可以修改
        //相当于const Person * const this
	}

	int m_a;
    mutable int m_b;//这个变量可以在常函数内修改
};

void test01()
{
	Person p;
	p.showPerson();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

常对象：

1.常对象可以访问常函数

2.常对象对成员变量的值不能修改，但是可以访问

3.常对象对mutable类对象的值可以修改。





### 4.4友元

在程序里，有些私有属性 也想让类外特殊的一些函数或者类进行访问，就需要用到友元的技术

友元的目的就是让一个函数或者类 访问另一个类中私有成员

友元的关键字为  ==friend==

友元的三种实现

* 全局函数做友元
* 类做友元
* 成员函数做友元



#### 4.4.1全局函数做友元

```c++
class Building
{
	//告诉编译器 goodGay全局函数 是 Building类的好朋友，可以访问类中的私有内容
	friend void goodGay(Building * building);
public:
	Building()
	{
		this->m_SittingRoom = "客厅";
		this->m_BedRoom = "卧室";
	}
public:
	string m_SittingRoom; //客厅
private:
	string m_BedRoom; //卧室
};

void goodGay(Building * building)
{
	cout << "好基友正在访问： " << building->m_SittingRoom << endl;
	cout << "好基友正在访问： " << building->m_BedRoom << endl;
}

void test01()
{
	Building b;
	goodGay(&b);
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

1.在类中使用关键字friend

2.关键字后粘贴复制全局函数的声明即可，声明后即可通过全局函数访问到类内的私有成员

#### 4.4.2类做友元

```c++
#include <iostream>
#include <string>
using namespace std;

class Building;
class GoodGay
{
public:
	//在GoodGay类中创造一个Building类指针
	GoodGay();
	//访问Building类中数据
	void visit();
private:
	Building* building;
};

class Building
{
	//声明GoodGay为友元类，可以访问Building类中数据
	friend class GoodGay;
public:
	Building();
public:
	string SittingRoom;
private:
	string BedRoom;

};

//给building类中数据赋初值
Building::Building()
{
	SittingRoom = "客厅";
	BedRoom = "厨房";
}

//基友类创造一个building类指针
GoodGay::GoodGay()
{
	building = new Building;
}

//基友访问building类中数据函数
void GoodGay::visit()
{
	cout << "好基友正在访问：" << building->SittingRoom << endl;
	cout << "好基友正在访问：" << building->BedRoom << endl;
}

//测试函数,创造一个基友类，基友类会自动生成一个building类指针
//通过访问visit函数，访问building类中数据
void test01()
{
	GoodGay g;
	g.visit();
}

//主函数，通过测试函数test01()调用类做友元功能
int main()
{
	test01();
	system("pause");
	return 0;
}
```

1.在类中使用friend关键字

2.在关键字后加上对应的类声明

3.使用类域对函数进行声明作用时，要在使用的类下面，否则声明的函数无法实现



#### 4.4.3成员函数做友元

```c++
#include <iostream>
#include <string>
using namespace std;


class Building;
class GoodGay
{
public:
	GoodGay();
	void visit01();
	void visit02();
private:
	Building* building;
};

class Building
{
	friend void GoodGay::visit01();
public:
	Building();
public:
	string SittingRoom;
private:
	string BedRoom;
};

Building::Building()
{
	SittingRoom = "客厅";
	BedRoom = "卧室";
}

GoodGay::GoodGay()
{
	building = new Building;
}

void GoodGay::visit01()
{
	cout << "visit01正在访问：" << building->SittingRoom << endl;
	cout << "visit01正在访问：" << building->BedRoom << endl;

}

void GoodGay::visit02()
{
	cout << "visit02正在访问：" << building->SittingRoom << endl;
	//cout << "visit02正在访问：" << building->BedRoom << endl;
}

void test01()
{
	GoodGay g;
	g.visit01();
	g.visit02();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

1.在Building类中使用friend关键字

2.在friend后面加上对应的函数声明，即可访问私人成员变量





### 4.5运算符重载



运算符重载概念：对已有的运算符重新进行定义，赋予其另一种功能，以适应不同的数据类型



#### 4.5.1加号运算符重载

实现自定义数据类型的相加运算，可以有成员函数实现和全局函数实现两项

无论是哪种实现都要使用operator+作为函数的名称，二者的使用方式都可以使用+号来代替

如果想使用各个函数代表的函数名来实现也是可以的

1.成员函数实现：

```c++
#include <iostream>
#include <string>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
public:
	//1.成员函数运算符重载：
	Person operator+(Person& p)
	{
		Person temp;
		temp.m_a = this->m_a + p.m_a;
		temp.m_b = this->m_b + p.m_b;
		return temp;
	}
};

void test01()
{
	Person p1;
	p1.m_a = 1;
	p1.m_b = 2;
	Person p2;
	p2.m_a = 3;
	p2.m_b = 4;
	//1.成员函数运算符重载本质：
	Person p3 = p1.operator+(p2);
	//Person p3 = p1 + p2;
	cout << "p3.m_a=" << p3.m_a << endl;
	cout << "p3.m_b=" << p3.m_b << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



2.全局函数实现：

```c++
#include <iostream>
#include <string>
using namespace std;
class Person
{
public:
	int m_a;
	int m_b;
};

//2.全局函数运算符重载
Person operator+(Person& p1, Person& p2)
{
	Person temp;
	temp.m_a = p1.m_a + p2.m_a;
	temp.m_b = p1.m_b + p2.m_b;
	return temp;
}


void test01()
{
	Person p1;
	p1.m_a = 1;
	p1.m_b = 2;
	Person p2;
	p2.m_a = 3;
	p2.m_b = 4;
	//2.全局函数运算符重载本质：
	Person p3 = operator+(p1, p2);
	//Person p3 = p1 + p2;
	cout << "p3.m_a=" << p3.m_a << endl;
	cout << "p3.m_b=" << p3.m_b << endl;
}
int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.5.2左移运算符重载

作用：可以输出自定义的数据类型’

1.使用左移运算符重载时，要使用**ostream**关键字作为返回值类型

2.返回值要用引用的形式

3.函数内部要有引用的ostream类型，因为是引用，所以其中的名字可以不是cout。

4.左移运算符的重载经常为**全局函数**而不是成员函数

5.为了访问私有内容，可以使用友元关键字

```c++
#include <iostream>
#include <string>
using namespace std;

class Person
{
	friend ostream& operator<<(ostream& cout, Person& p);
public:
	Person(int a, int b)
	{
		m_a = a;
		m_b = b;
	}
private:
	int m_a;
	int m_b;
};

//左移运算符重载;
ostream& operator<<(ostream& cout, Person& p)
{
	cout << "a=" << p.m_a << " b=" << p.m_b;
	return cout;
}

void test01()
{
	Person p(10, 20);
	cout << p << " hello world " << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.5.3递增运算符重载

作用：通过重载递增运算符，实现自己的整型数据

1.前置递增返回引用，后置递增返回值

前置递增：

```c++
#include <iostream>
using namespace std;


class Person
{
public:
    //左移运算符直接输出类
	friend ostream& operator<<(ostream& cout, Person p);
	Person(int a)
	{
		m_a = a;
	}
	//前置++运算符重载,返回引用
	Person& operator++()
	{
		++m_a;
		return *this;
	}
private:
	int m_a;
};

//左移运算符重载：
ostream& operator<<(ostream& cout, Person p)
{
	cout << "a=" << p.m_a;
	return cout;
}

//前置++运算
void test01()
{
	Person p1(10);
	cout << ++(++p1) << endl;
	cout << p1;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

前置必须要返回引用，否则p1的值不会二次改变

后置递增：

```c++
#include <iostream>
using namespace std;
class Person
{
public:
	friend ostream& operator<<(ostream& cout, Person p);
	Person(int a)
	{
		m_a = a;
	}
	//后置++运算符重载，返回值，括号内必须有int进行占位
	Person operator++(int)
	{
		Person temp = *this;
		m_a++;
		return temp;
	}
private:
	int m_a;
};

//左移运算符重载：
ostream& operator<<(ostream& cout, Person p)
{
	cout << "a=" << p.m_a;
	return cout;
}

//后置++运算
void test02()
{
	Person p2(10);
	cout << p2++ << endl;
	cout << p2 << endl;
}

int main()
{
	test02();
	system("pause");
	return 0;
}
```



#### 4.5.4赋值运算符重载



```c++
#include <iostream>

using namespace std;

class Person
{
public:
	//接受年龄的析构函数
	Person(int a)
	{
		m_age = new int(a);
	}

	//赋值运算符重载：
	Person& operator=(Person &p)
	{
		//首先判断自身的年龄指针是否为空，不是的话要释放
		if (m_age != NULL)
		{
			delete m_age;
			m_age = NULL;
		}
		//在堆区新开辟一个空间存放数据
		m_age = new int(*p.m_age);
		//为了使赋值操作可以多次重复进行，需要返回本身
		return *this;
	}

	//对于新开辟的指针，如果不为空则释放
	~Person()
	{
		if (m_age != NULL)
		{
			delete m_age;
			m_age = NULL;
		}
	}

public:
	//创造一个年龄的指针用来接受年龄
	int *m_age;
};

void test01()
{
	Person p1(10);
	Person p2(20);
	Person p3(30);
	p2 = p1;
	cout << "p1的年龄为：" << *p1.m_age << endl;
	cout << "p2的年龄为：" << *p2.m_age << endl;
	cout << "p3的年龄为：" << *p3.m_age << endl;
	p3 = p2 = p1;
	cout << "p1的年龄为：" << *p1.m_age << endl;
	cout << "p2的年龄为：" << *p2.m_age << endl;
	cout << "p3的年龄为：" << *p3.m_age << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.5.5关系运算符重载



```c++
#include <iostream>
#include <string>

using namespace std;

class Person
{
public:
	//通过析构函数对名字和年龄进行赋值
	Person(string name, int age)
	{
		m_name = name;
		m_age = age;
	}
	//==号重载，如果二者相同返回真，二者不同返回假
	bool operator==(Person &p)
	{
		if (this->m_age == p.m_age && this->m_name == p.m_name)
		{
			return true;
		}
		return false;
	}
	//!=号重载，如果二者相同返回假，二者不同返回真
	bool operator!=(Person& p)
	{
		if (this->m_age == p.m_age && this->m_name == p.m_name)
		{
			return false;
		}
		return true;
	}
public:
	string m_name;
	int m_age;
};

void test01()
{
	Person p1("张三", 18);
	Person p2("张三", 18);
	if (p1 == p2)
	{
		cout << "二者相同" << endl;
	}
	else
	{
		cout << "二者不同" << endl;
	}
	if (p1 != p2)
	{
		cout << "二者不同" << endl;
	}
	else
	{
		cout << "二者相同" << endl;
	}
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.5.6函数调用运算符重载



* 函数调用运算符 ()  也可以重载
* 由于重载后使用的方式非常像函数的调用，因此称为仿函数
* 仿函数没有固定写法，非常灵活



```c++
#include <iostream>
#include <string>

using namespace std;

class MyPrint
{
public:
	//重载的（）操作符 也称为仿函数
	void operator()(string text)
	{
		cout << text << endl;
	}
};

void test01()
{
	MyPrint M1;
	M1("张三");
}

class MyAdd
{
public:
	int operator()(int a, int b)
	{
		return a + b;
	}
};

void test02()
{
	MyAdd M2;
	cout << M2(1, 2) << endl;
	//匿名函数调用：
	cout << MyAdd()(2, 2) << endl;
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

1.函数调用时可以使用匿名函数调用方式





### 4.6继承

#### 4.6.1继承的基本语法

继承的好处：==可以减少重复的代码==

class A : public B; 

A 类称为子类 或 派生类

B 类称为父类 或 基类



**派生类中的成员，包含两大部分**：

一类是从基类继承过来的，一类是自己增加的成员。

从基类继承过过来的表现其共性，而新增的成员体现了其个性。



```c++
#include <iostream>
#include <string>

using namespace std;


//生成父类（基类），在父类中输出相同的信息
class BasePoint
{
public:
	void header()
	{
		cout << "顶部" << endl;
	}
	void footer()
	{
		cout << "底部" << endl;
	}
	void left()
	{
		cout << "左侧" << endl;
	}
};

//生成子类（派生类），在子类中输出不同的信息

//Java页面：
class Jave :public BasePoint
{
public:
	void content()
	{
		cout << "Java页面" << endl;
	}
};

//Python页面：
class Python :public BasePoint
{
public:
	void content()
	{
		cout << "Python页面" << endl;
	}
};

//CPP页面：
class CPP :public BasePoint
{
public:
	void content()
	{
		cout << "CPP页面" << endl;
	}
};

void test01()
{
	Jave J;
	Python P;
	CPP C;

	cout << "----------------------" << endl;
	J.header();
	J.footer();
	J.left();
	J.content();

	cout << "----------------------" << endl;
	P.header();
	P.footer();
	P.left();
	P.content();

	cout << "----------------------" << endl;
	C.header();
	C.footer();
	C.left();
	C.content();
	cout << "----------------------" << endl;

}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.6.2继承方式

继承的语法：`class 子类 : 继承方式  父类`



**继承方式一共有三种：**

* 公共继承
* 保护继承
* 私有继承





![img](D:\计算机自学\C++\黑马程序员\原文件\匠心精作C++从0到1入门编程-学习编程不再难资料\第3阶段-C++核心编程 资料\讲义\assets\clip_image002.png)





#### 4.6.3继承中的对象模型



父类中私有成员也是被子类继承下去了，只是由编译器给隐藏后访问不到



```c++
class Base
{
public:
	int m_A;
protected:
	int m_B;
private:
	int m_C; //私有成员只是被隐藏了，但是还是会继承下去
};

//公共继承
class Son :public Base
{
public:
	int m_D;
};

void test01()
{
	cout << "sizeof Son = " << sizeof(Son) << endl;//输出16
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.6.4继承中构造和析构顺序



继承中 先调用父类构造函数，再调用子类构造函数，析构顺序与构造相反



#### 4.6.5继承同名成员处理方式

* 访问子类同名成员   直接访问即可
* 访问父类同名成员   需要加作用域

1. 子类对象可以直接访问到子类中同名成员
2. 子类对象加作用域可以访问到父类同名成员
3. 当子类与父类拥有同名的成员函数，子类会隐藏父类中同名成员函数，加作用域可以访问到父类中同名函数



```c++
class Base {
public:
	Base()
	{
		m_A = 100;
	}
	void func()
	{
		cout << "Base - func()调用" << endl;
	}
	void func(int a)
	{
		cout << "Base - func(int a)调用" << endl;
	}
public:
	int m_A;
};

class Son : public Base {
public:
	Son()
	{
		m_A = 200;
	}
	//当子类与父类拥有同名的成员函数，子类会隐藏父类中所有版本的同名成员函数
	//如果想访问父类中被隐藏的同名成员函数，需要加父类的作用域
	void func()
	{
		cout << "Son - func()调用" << endl;
	}
public:
	int m_A;
};

void test01()
{
	Son s;
	cout << "Son下的m_A = " << s.m_A << endl;
	cout << "Base下的m_A = " << s.Base::m_A << endl;

	s.func();
	s.Base::func();
	s.Base::func(10);
}
int main()
{
	test01();
	system("pause");
	return EXIT_SUCCESS;
}
```



#### 4.6.6继承同名静态成员处理方式



静态成员和非静态成员出现同名，处理方式一致



- 访问子类同名成员   直接访问即可
- 访问父类同名成员   需要加作用域

同名静态成员处理方式和非静态处理方式一样，只不过有两种访问的方式（通过对象 和 通过类名）

```c++
class Base 
{
public:
	static void func()
	{
		cout << "Base - static void func()" << endl;
	}
	static void func(int a)
	{
		cout << "Base - static void func(int a)" << endl;
	}
	static int m_A;
};

int Base::m_A = 100;

class Son : public Base 
{
public:
	static void func()
	{
		cout << "Son - static void func()" << endl;
	}
	static int m_A;
};

int Son::m_A = 200;

//同名成员属性
void test01()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	cout << "Son  下 m_A = " << s.m_A << endl;
	cout << "Base 下 m_A = " << s.Base::m_A << endl;

	//通过类名访问
	cout << "通过类名访问： " << endl;
	cout << "Son  下 m_A = " << Son::m_A << endl;
	cout << "Base 下 m_A = " << Son::Base::m_A << endl;
}

//同名成员函数
void test02()
{
	//通过对象访问
	cout << "通过对象访问： " << endl;
	Son s;
	s.func();
	s.Base::func();

	cout << "通过类名访问： " << endl;
	Son::func();
	Son::Base::func();
	//出现同名，子类会隐藏掉父类中所有同名成员函数，需要加作作用域访问
	Son::Base::func(100);
}
int main()
{
	//test01();
	test02();
	system("pause");
	return 0;
}
```



#### 4.6.7多继承语法



C++允许**一个类继承多个类**

语法：` class 子类 ：继承方式 父类1 ， 继承方式 父类2...`

多继承可能会引发父类中有同名成员出现，需要加作用域区分

**C++实际开发中不建议用多继承**



#### 4.6.8菱形继承

**菱形继承概念：**

​	两个派生类继承同一个基类

​	又有某个类同时继承者两个派生类

​	这种继承被称为菱形继承，或者钻石继承

**典型的菱形继承案例：**



![IMG_256](D:\计算机自学\C++\黑马程序员\原文件\匠心精作C++从0到1入门编程-学习编程不再难资料\第3阶段-C++核心编程 资料\讲义\assets\clip_image002.jpg)



**菱形继承问题：**

1.     羊继承了动物的数据，驼同样继承了动物的数据，当草泥马使用数据时，就会产生二义性。

2.     草泥马继承自动物的数据继承了两份，其实我们应该清楚，这份数据我们只需要一份就可以。



```c++
class Animal
{
public:
	int m_Age;
};

//继承前加virtual关键字后，变为虚继承
//此时公共的父类Animal称为虚基类
class Sheep : virtual public Animal {};
class Tuo   : virtual public Animal {};
class SheepTuo : public Sheep, public Tuo {};

void test01()
{
	SheepTuo st;
	st.Sheep::m_Age = 100;
	st.Tuo::m_Age = 200;

	cout << "st.Sheep::m_Age = " << st.Sheep::m_Age << endl;
	cout << "st.Tuo::m_Age = " <<  st.Tuo::m_Age << endl;
	cout << "st.m_Age = " << st.m_Age << endl;
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：

* 菱形继承带来的主要问题是子类继承两份相同的数据，导致资源浪费以及毫无意义
* 利用虚继承可以解决菱形继承问题
* 不建议使用菱形继承





### 4.7多态



#### 4.7.1多态的基本概念



**多态是C++面向对象三大特性之一**

多态分为两类

* 静态多态: 函数重载 和 运算符重载属于静态多态，复用函数名
* 动态多态: 派生类和虚函数实现运行时多态



静态多态和动态多态区别：

* 静态多态的函数地址早绑定  -  编译阶段确定函数地址
* 动态多态的函数地址晚绑定  -  运行阶段确定函数地址



```c++
class Animal
{
public:
	//Speak函数就是虚函数
	//函数前面加上virtual关键字，变成虚函数，那么编译器在编译的时候就不能确定函数调用了。
	virtual void speak()
	{
		cout << "动物在说话" << endl;
	}
};

class Cat :public Animal
{
public:
	void speak()
	{
		cout << "小猫在说话" << endl;
	}
};

class Dog :public Animal
{
public:

	void speak()
	{
		cout << "小狗在说话" << endl;
	}

};
//我们希望传入什么对象，那么就调用什么对象的函数
//如果函数地址在编译阶段就能确定，那么静态联编
//如果函数地址在运行阶段才能确定，就是动态联编

void DoSpeak(Animal & animal)
{
	animal.speak();
}
//
//多态满足条件： 
//1、有继承关系
//2、子类重写父类中的虚函数
//多态使用：
//父类指针或引用指向子类对象

void test01()
{
	Cat cat;
	DoSpeak(cat);

	Dog dog;
	DoSpeak(dog);
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：

多态满足条件

* 有继承关系
* 子类重写父类中的虚函数

多态使用条件

* 父类指针或引用指向子类对象

==重写：函数返回值类型  函数名 参数列表 完全一致称为重写==





#### 4.7.2多态案例一.计算器类



多态的优点：

* 代码组织结构清晰
* 可读性强
* 利于前期和后期的扩展以及维护



```c++
#include <iostream>
#include <string>
using namespace std;

//普通计算器类
class Calulator
{
public:
	//通过获得的字符来判断执行什么操作
	int getResult(string oper)
	{
		//加法
		if (oper == "+")
		{
			return m_Num1 + m_Num2;
		}
		//减法
		else if (oper == "-")
		{
			return m_Num1 - m_Num2;
		}
		//乘法
		else if (oper == "*")
		{
			return m_Num1 * m_Num2;
		}
	}
//定义两个数字
public:
	int m_Num1 = 0;
	int m_Num2 = 0;
};

//普通类计算器实现
void test01()
{
	Calulator C;
	C.m_Num1 = 1;
	C.m_Num2 = 2;
	cout << C.m_Num1 << "+" << C.m_Num2 << "=" << C.getResult("+") << endl;

}

//多态计算器类实现
class AbstractCalulator
{
public:
	virtual int getResult()
	{
		return 0;
	}
	int m_Num1 = 0;
	int m_Num2 = 0;
};

//多态加法计算器
class AddCalulator :public AbstractCalulator
{
public:
	int getResult()
	{
		return m_Num1 + m_Num2;
	}
};

//多态减法计算器
class SubCalulator :public AbstractCalulator
{
public:
	int getResult()
	{
		return m_Num1 - m_Num2;
	}
};

//多态乘法计算器
class MulCalulator :public AbstractCalulator
{
	int getResult()
	{
		return m_Num1 * m_Num2;
	}
};

//多态类计算器实现
void test02()
{
	//多态类加法计算
	AbstractCalulator* abc = new AddCalulator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 20;
	cout << abc->m_Num1 << "+" << abc->m_Num2 << "=" << abc->getResult() << endl;
	delete abc;

	//多态类减法计算器
	abc = new SubCalulator;
	abc->m_Num1 = 10;
	abc->m_Num2 = 20;
	cout << abc->m_Num1 << "-" << abc->m_Num2 << "=" << abc->getResult() << endl;
	delete abc;

	//多态类乘法计算器
	abc = new MulCalulator;
	abc->m_Num1 = 2;
	abc->m_Num2 = 4;
	cout << abc->m_Num1 << "*" << abc->m_Num2 << "=" << abc->getResult() << endl;

}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

总结：C++开发提倡利用多态设计程序架构，因为多态优点很多



#### 4.7.3纯虚函数和抽象类

在多态中，通常父类中虚函数的实现是毫无意义的，主要都是调用子类重写的内容

因此可以将虚函数改为**纯虚函数**

纯虚函数语法：`virtual 返回值类型 函数名 （参数列表）= 0 ;`

当类中有了纯虚函数，这个类也称为==抽象类==，抽象类无法实例化对象

**抽象类特点**：

 * 无法实例化对象
 * 子类必须重写抽象类中的纯虚函数，否则也属于抽象类



```c++
#include <iostream>
using namespace std;

//创建纯虚类
class Base
{
public:
	virtual void func() = 0;
};

//创建子类并继承和多态
class Son :public Base
{
public:
	virtual void func()
	{
		cout << "func函数的调用" << endl;
	}
};

void test01()
{
	Base* base = NULL;
	base = new Son;
	base->func();
	delete base;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```





#### 4.7.4多态案例二.制作饮品



```c++
#include <iostream>
#include <string>
using namespace std;

//制作抽象类
class AbstracrRinking
{
//在抽象类中定义纯虚函数，四个函数分别为：
//1.烧水	2.冲泡	3.倒入杯中	4.加入辅料
public:
	//1.烧水
	virtual void Boil() = 0;
	//2.冲泡
	virtual void Brew() = 0;
	//3.倒入杯中
	virtual void PourInCup() = 0;
	//4.加入辅料
	virtual void PutSomething() = 0;
//规定流程
public:
	void MakeDrink()
	{
		Boil();
		Brew();
		PourInCup();
		PutSomething();
	}
};

//制作咖啡类
class Coffee :public AbstracrRinking
{
//在咖啡类中重新定义四个虚函数
public:
	virtual void Boil()
	{
		cout << "煮农夫山泉" << endl;
	}
	virtual void Brew()
	{
		cout << "冲泡咖啡" << endl;
	}
	virtual void PourInCup()
	{
		cout << "将咖啡倒入杯中" << endl;
	}
	virtual void PutSomething()
	{
		cout << "加入牛奶" << endl;
	}
};

//制作茶类
class Tea :public AbstracrRinking
{
public:
	virtual void Boil()
	{
		cout << "煮白开水" << endl;
	}
	virtual void Brew()
	{
		cout << "冲泡茶叶" << endl;
	}
	virtual void PourInCup()
	{
		cout << "将茶倒入杯中" << endl;
	}
	virtual void PutSomething()
	{
		cout << "加入枸杞" << endl;
	}
};
//调用测试函数
void Dowork(AbstracrRinking *abs)
{
	abs->MakeDrink();
	delete abs;
}

//调用测试函数
void test01()
{
	//首先调用茶类,传入茶类new指针，通过函数来用抽象类指针接受这个new指针
	Dowork(new Tea);
	cout << "---------------" << endl;
	//调用咖啡类
	Dowork(new Coffee);
	cout << "---------------" << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 4.7.5虚析构和纯虚析构

多态使用时，如果子类中有属性开辟到堆区，那么父类指针在释放时无法调用到子类的析构代码

解决方式：将父类中的析构函数改为**虚析构**或者**纯虚析构**

虚析构和纯虚析构共性：

* 可以解决父类指针释放子类对象
* 都需要有具体的函数实现

虚析构和纯虚析构区别：

* 如果是纯虚析构，该类属于抽象类，无法实例化对象

虚析构语法：

`virtual ~类名(){}`

纯虚析构语法：

` virtual ~类名() = 0;`

`类名::~类名(){}`

```c++
#include <iostream>
#include <string>

using namespace std;

class Animal
{
public:
	virtual void Speak() = 0;
	Animal()
	{
		cout << "Animal构造函数调用" << endl;
	}

	//虚析构函数调用
	/*virtual ~Animal()
	{
		cout << "Animal析构函数调用" << endl;
	}*/
	//纯虚析构函数调用
	virtual ~Animal() = 0;
};
Animal::~Animal()
{
	cout << "Animal析构函数调用" << endl;
}

class Cat :public Animal
{
public:
	virtual void Speak()
	{
		cout << "小猫在说话" << endl;
	}
	Cat(string name)
	{
		cout << "Cat构造函数调用" << endl;
		m_Name = new string(name);
	}
	~Cat()
	{
		if (m_Name != NULL)
		{
			delete m_Name;
			m_Name = NULL;
		}
		cout << "Cat析构函数调用" << endl;
	}

public:
	string* m_Name;
};

void test01()
{
	Animal* animal = new Cat("Tom");
	animal->Speak();
	delete animal;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：

​	1. 虚析构或纯虚析构就是用来解决通过父类指针释放子类对象

​	2. 如果子类中没有堆区数据，可以不写为虚析构或纯虚析构

​	3. 拥有纯虚析构函数的类也属于抽象类



#### 4.7.6多态案例三.电脑组装



```c++
#include <iostream>
#include <string>

using namespace std;

//创建CPU类
class CPU
{
public:
	virtual void calulate() = 0;
};

//创建显卡类
class VideoCard
{
public:
	virtual void display() = 0;
};

//创建内存条类
class Memory
{
public:
	virtual void storage() = 0;
};

//创建电脑类
class Computer
{
	//通过接受三个元件的指针来使电脑进行工作
public:
	Computer(CPU* cpu, VideoCard* vc, Memory* mem)
	{
		m_cpu = cpu;
		m_vc = vc;
		m_mem = mem;
	}
	//提供工作函数
	void work()
	{
		m_cpu->calulate();
		m_vc->display();
		m_mem->storage();
	}
	//提供CPU函数，释放3个电脑零件
	~Computer()
	{
		if (m_cpu != NULL)
		{
			delete m_cpu;
			m_cpu = NULL;
		}
		if (m_vc != NULL)
		{
			delete m_vc;
			m_vc = NULL;
		}
		if (m_mem != NULL)
		{
			delete m_mem;
			m_mem = NULL;
		}
	}
	//对电脑中的三个零件信息进行私有化指针处理
private:
	CPU* m_cpu;
	VideoCard* m_vc;
	Memory* m_mem;
};

//Intel厂商组装
class IntelCPU :public CPU
{
	virtual void calulate()
	{
		cout << "Intel的CPU开始计算" << endl;
	}
};
class IntelVideoCard :public VideoCard
{
	virtual void display()
	{
		cout << "Intel的显卡开始显示了" << endl;
	}
};
class IntelMemory :public Memory
{
	virtual void storage()
	{
		cout << "Intel的内存条开始存储了" << endl;
	}
};

//Lenovo厂商
class LenovoCPU :public CPU
{
	virtual void calulate()
	{
		cout << "Lenovo的CPU开始计算" << endl;
	}
};
class LenovoVideoCard :public VideoCard
{
	virtual void display()
	{
		cout << "Lenovo的显卡开始显示了" << endl;
	}
};
class LenovoMemory :public Memory
{
	virtual void storage()
	{
		cout << "Lenovo的内存条开始存储了" << endl;
	}
};

void test01()
{
	cout << "-----------------------------" << endl;
	//第一台电脑零件
	CPU* intelCpu = new IntelCPU;
	VideoCard* intelCard = new IntelVideoCard;
	Memory* intelMem = new IntelMemory;
	cout << "第一台电脑开始工作" << endl;
	Computer* computer1 = new Computer(intelCpu, intelCard, intelMem);
	computer1->work();
	computer1;
	cout << "-----------------------------" << endl;
	cout << "第二台电脑开始工作" << endl;
	Computer* computer2 = new Computer(new LenovoCPU, new LenovoVideoCard, new LenovoMemory);
	computer2->work();
	delete computer2;
	cout << "-----------------------------" << endl;
	cout << "第三台电脑开始工作" << endl;
	Computer* computer3 = new Computer(new IntelCPU, new LenovoVideoCard, new IntelMemory);
	computer3->work();
	delete computer3;
	cout << "-----------------------------" << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```





## 5.文件操作





程序运行时产生的数据都属于临时数据，程序一旦运行结束都会被释放

通过**文件可以将数据持久化**

C++中对文件操作需要包含头文件 ==&lt; fstream &gt;==



文件类型分为两种：

1. **文本文件**     -  文件以文本的**ASCII码**形式存储在计算机中
2. **二进制文件** -  文件以文本的**二进制**形式存储在计算机中，用户一般不能直接读懂它们



操作文件的三大类:

1. ofstream：写操作
2. ifstream： 读操作
3. fstream ： 读写操作



### 5.1文本文件

#### 5.1.1写文件



   写文件步骤如下：

1. 包含头文件   

   \#include <fstream\>

2. 创建流对象  

   ofstream ofs;

3. 打开文件

   ofs.open("文件路径",打开方式);

4. 写数据

   ofs << "写入的数据";

5. 关闭文件

   ofs.close();

   

文件打开方式：

| 打开方式    | 解释                       |
| ----------- | -------------------------- |
| ios::in     | 为读文件而打开文件         |
| ios::out    | 为写文件而打开文件         |
| ios::ate    | 初始位置：文件尾           |
| ios::app    | 追加方式写文件             |
| ios::trunc  | 如果文件存在先删除，再创建 |
| ios::binary | 二进制方式                 |

**注意：** 文件打开方式可以配合使用，利用|操作符

**例如：**用二进制方式写文件 `ios::binary |  ios:: out`



示例：

```c++
#include <iostream>
#include <fstream>

using namespace std;

void test01()
{
	ofstream ofs;
	ofs.open("test.txt", ios::out);
	ofs << "姓名：张三" << endl;
	ofs << "性别：男" << endl;
	ofs << "年龄：18" << endl;
	ofs.close();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



总结：

* 文件操作必须包含头文件 fstream
* 读文件可以利用 ofstream  ，或者fstream类
* 打开文件时候需要指定操作文件的路径，以及打开方式
* 利用<<可以向文件中写数据
* 操作完毕，要关闭文件



#### 5.1.2读文件



读文件与写文件步骤相似，但是读取方式相对于比较多



读文件步骤如下：

1. 包含头文件   

   \#include <fstream\>

2. 创建流对象  

   ifstream ifs;

3. 打开文件并判断文件是否打开成功

   ifs.open("文件路径",打开方式);

4. 读数据

   四种方式读取

5. 关闭文件

   ifs.close();



示例：

```c++
#include <iostream>
#include <fstream>
#include <string>
using namespace std;


void test01()
{
	ifstream ifs;
	ifs.open("test.txt", ios::in);
	if (!ifs.is_open())
	{
		cout << "文件打开失败" << endl;
		return;
	}

	//四种读取方式：
	//第一种
	/*char buf[1024] = { 0 };
	while (ifs >> buf)
	{
		cout << buf << endl;
	}*/

	//第二种
	/*char buf[1024] = { 0 };
	while (ifs.getline(buf, sizeof(buf)))
	{
		cout << buf << endl;
	}*/

	//第三种
	//string buf;
	//while (getline(ifs, buf))
	//{
	//	cout << buf << endl;
	//}

	//第四种
	char c;
	while ((c = ifs.get()) != EOF)
	{
		cout << c;
	}
	ifs.close();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



总结：

- 读文件可以利用 ifstream  ，或者fstream类
- 利用is_open函数可以判断文件是否打开成功
- close 关闭文件 



一共有四种读取方式：

第一种：

```c++
char buf[1024] = { 0 };
while (ifs >> buf)
{
	cout << buf << endl;
}
```



第二种：

```c++
char buf[1024] = { 0 };
while (ifs.getline(buf, sizeof(buf)))
{
	cout << buf << endl;
}
```



第三种：

```c++
string buf;
while (getline(ifs, buf))
{
	cout << buf << endl;
}
```



第四种：

```c++
char c;
while ((c = ifs.get()) != EOF)
{
	cout << c;
}
```





### 5.2二进制文件

以二进制的方式对文件进行读写操作

打开方式要指定为 ==ios::binary==

#### 5.2.1写文件

二进制方式写文件主要利用流对象调用成员函数write

函数原型 ：`ostream& write(const char * buffer,int len);`

参数解释：字符指针buffer指向内存中一段存储空间。len是读写的字节数



示例：

```c++
#include <iostream>
#include <string>
#include <fstream>

using namespace std;

class Person
{
public:
	char m_Name[64];
	int m_Age;
};


void test01()
{
	Person p = { "张三",18 };
	ofstream ofs("person.txt", ios::out|ios::binary);

	ofs.write((const char*)&p, sizeof(p));

	ofs.close();
}

int main() {

	test01();
	system("pause");
	return 0;
}
```

总结：

* 文件输出流对象 可以通过write函数，以二进制方式写数据





#### 5.2.2读文件



二进制方式读文件主要利用流对象调用成员函数read

函数原型：`istream& read(char *buffer,int len);`

参数解释：字符指针buffer指向内存中一段存储空间。len是读写的字节数

示例：

```c++
#include <iostream>
#include <fstream>

using namespace std;

class Person
{
public:
	char m_Name[64];
	int m_Age;
};

void test01()
{
	ifstream ifs("person.txt", ios::in | ios::binary);
	if (!ifs.is_open())
	{
		cout << "文件打开失败" << endl;
		return;
	}
	Person p;
	ifs.read((char*)&p, sizeof(p));
	cout << "姓名：" << p.m_Name << " 年龄：" << p.m_Age << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



文件输入流对象 可以通过read函数，以二进制方式读数据





# 三.C++提高编程



## 1.模板

### 1.1模板的概念

模板就是建立**通用的模具**，大大**提高复用性**

模板的特点：

* 模板不可以直接使用，它只是一个框架
* 模板的通用并不是万能的





### 1.2函数模板



* C++另一种编程思想称为 ==泛型编程== ，主要利用的技术就是模板


* C++提供两种模板机制:**函数模板**和**类模板** 



#### 1.2.1 函数模板语法

函数模板作用：

建立一个通用函数，其函数返回值类型和形参类型可以不具体制定，用一个**虚拟的类型**来代表。

**语法：** 

```C++
template<typename T>
函数声明或定义
```

**解释：**

template  ---  声明创建模板

typename  --- 表面其后面的符号是一种数据类型，可以用class代替

T    ---   通用的数据类型，名称可以替换，通常为大写字母



示例：

```c++
#include <iostream>

using namespace std;


//利用模板提供通用的交换函数
template<typename T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;

}

void test01()
{
	int a = 10;
	int b = 20;
    //1.自动类型推导
    //mySwap(a,b);
    
    //2.显示指定类型
	mySwap<int>(a, b);
	cout << "a=" << a << endl;
	cout << "b=" << b << endl;

}


int main()
{
	test01();
	system("pause");
	return 0;
}
```



总结：

* 函数模板利用关键字 template
* 使用函数模板有两种方式：自动类型推导、显示指定类型
* 模板的目的是为了提高复用性，将类型参数化



#### 1.2.2函数模板注意事项

注意事项：

* 自动类型推导，必须推导出一致的数据类型T,才可以使用


* 模板必须要确定出T的数据类型，才可以使用



示例：

```c++
#include <iostream>

using namespace std;

//1.自动类型推导，必须推导出一致的数据类型T，才可以使用
//利用模板提供通用的交换函数
template<class T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

void test01()
{
	int a = 10;
	int b = 20;
	char c = 'a';
	mySwap(a, b);	//正确，可以推导出一致的T类型
	//mySwap(a,c);	//错误，推导不出一致的T类型
}

//2.模板必须要确定出T的数据类型，才可以使用
template<class T>
void func()
{
	cout << "func()的调用" << endl;
}

void test02()
{
	//func();//错误，模板不能独立使用，必须确定T的类型
	func<int>();
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

总结：

* 使用模板时必须确定出通用数据类型T，并且能够推导出一致的类型



#### 1.2.3函数模板案例

案例描述：

* 利用函数模板封装一个排序的函数，可以对**不同数据类型数组**进行排序
* 排序规则从大到小，排序算法为**选择排序**
* 分别利用**char数组**和**int数组**进行测试



示例：

```c++
#include <iostream>

using namespace std;

//模板交换函数
template<class T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}

//模板排序函数
template<class T>
void mySort(T arr[], int len)
{
	for (int i = 0; i < len; i++)
	{
		int max = i;
		for (int j = i+1; j < len; j++)
		{
			if (arr[max] < arr[j])
			{
				max = j;
			}
		}
		if (max != i)
		{
			mySwap(arr[max], arr[i]);
		}
	}
}

//模板输出函数
template<class T>
void printArray(T arr[], int len)
{
	for (int i = 0; i < len; i++)
	{
		cout << arr[i] << " ";
	}
	cout << endl;
}


//测试char数组
void test01()
{
	char charArr[] = "bdcfeagh";
	int len = sizeof(charArr) / sizeof(char);
	mySort(charArr, len);
	printArray(charArr, len);
}

//测试int数组
void test02()
{
	int intArr[] = { 7,5,8,1,3,9,2,4,6 };
	int len = sizeof(intArr) / sizeof(int);
	mySort(intArr, len);
	printArray(intArr, len);
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
} 
```



#### 1.2.4普通函数与函数模板的区别



**普通函数与函数模板区别：**

* 普通函数调用时可以发生自动类型转换（隐式类型转换）
* 函数模板调用时，如果利用自动类型推导，不会发生隐式类型转换
* 如果利用显示指定类型的方式，可以发生隐式类型转换



示例：

```c++
#include <iostream>

using namespace std;

//普通函数
int myAdd01(int a, int b)
{
	return a + b;
}

//函数模板
template<class T>
T myAdd02(T a, T b)
{
	return a + b;
}

void test01()
{
	int a = 10;
	int b = 20;
	char c = 'c';
	cout << myAdd01(a, c) << endl;//正确，函数将char类型的'c'隐式转换为int类型'c'对应的ASCII码99
	//cout << myAdd02(a, c) << end;	//错误，使用自动类型推导时，不会发生隐式类型转换
	cout << myAdd02<int>(a, c) << endl;//正确，如果使用显示指定类型，可以发生隐式类型转换
}


int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：建议使用显示指定类型的方式，调用函数模板，因为可以自己确定通用类型T



#### 1.2.5普通函数与函数模板的调用规则



调用规则如下：

1. 如果函数模板和普通函数都可以实现，优先调用普通函数
2. 可以通过空模板参数列表来强制调用函数模板
3. 函数模板也可以发生重载
4. 如果函数模板可以产生更好的匹配,优先调用函数模板



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

void myPrint(int a, int b)
{
	cout << "调用的普通函数" << endl;
}

template<class T>
void myPrint(T a, T b)
{
	cout << "调用的模板" << endl;
}

template<class T>
void myPrint(T a, T b, T c)
{
	cout << "调用重载的模板" << endl;
}

void test01()
{
	//1.如果函数模板和普通函数都可以实现，优先调用普通函数
	//注意如果告诉编译器 普通函数是有的，但只是声明没有实现，或者不在当前文件内实现，就会报错找不到
	int a = 10;
	int b = 20;
	myPrint(a, b);	//调用普通函数

	//2.可以通过空模板参数列表来强调函数模板
	myPrint<>(a, b);	//调用函数模板

	//3.函数模板也可以发生重载
	int c = 30;
	myPrint(a, b, c);	//调用重载的函数模板

	//4.如果函数模板可以产生更好的匹配，有限调用函数模板
	char c1 = 'a';
	char c2 = 'b';
	char c3 = 'c';
	myPrint(c1, c2);	//调用函数模板
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：既然提供了函数模板，最好就不要提供普通函数，否则容易出现二义性



#### 1.2.6模板的局限性

**局限性：**

* 模板的通用性并不是万能的

**例如：**

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	a = b;
    }
```

在上述代码中提供的赋值操作，如果传入的a和b是一个数组，就无法实现了

再例如：

```C++
	template<class T>
	void f(T a, T b)
	{ 
    	if(a > b) { ... }
    }
```

在上述代码中，如果T的数据类型传入的是像Person这样的自定义数据类型，也无法正常运行

因此C++为了解决这种问题，提供模板的重载，可以为这些**特定的类型**提供**具体化的模板**

具体化模板需要重新自定义一次

示例：

```c++
#include <iostream>
#include <string>
using namespace std;

class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	string m_Name;
	int m_Age;
};

//普通函数模板
template<class T>
bool myCompare(T& a, T& b)
{
	if (a == b)
	{
		return true;
	}
	else
	{
		return false;
	}
}

//具体化，显示具体化的原型和定义以template<>开头，并通过名臣来指出类型
//具体化优先于常规模板
template<> bool myCompare(Person& p1, Person& p2)
{
	if (p1.m_Name == p2.m_Name && p1.m_Age == p2.m_Age)
	{
		return true;
	}
	else
	{
		return false;
	}
}

void test01()
{
	int a = 10;
	int b = 20;
	//内置数据类型可以直接使用通过的函数模板
	bool ret = myCompare(a, b);
	if (ret)
	{
		cout << "a==b" << endl;
	}
	else
	{
		cout << "a!=b" << endl;
	}
}

void test02()
{
	Person p1("Tom", 10);
	Person p2("Tom", 10);
	//自定义数据类型，不会调用普通的函数模板
	//可以创建具体化的Person数据类型的模板，用于特殊处理这个类型
	bool ret = myCompare(p1, p2);
	if (ret)
	{
		cout << "p1==p2" << endl;
	}
	else
	{
		cout << "p1!=p2" << endl;
	}
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

总结：

* 利用具体化的模板，可以解决自定义类型的通用化
* 学习模板并不是为了写模板，而是在STL能够运用系统提供的模板





### 1.3类模板

#### 1.3.1类模板语法

类模板作用：

* 建立一个通用类，类中的成员 数据类型可以不具体制定，用一个**虚拟的类型**来代表。



**语法：** 

```c++
template<typename T>
类
```

**解释：**

template  ---  声明创建模板

typename  --- 表面其后面的符号是一种数据类型，可以用class代替

T    ---   通用的数据类型，名称可以替换，通常为大写字母



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

template<class NameType,class AgeType>
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	void showPerson()
	{
		cout << "name: " << m_Name << " age: " << m_Age << endl;
	}

public:
	NameType m_Name;
	AgeType m_Age;
};


void test01()
{
	Person<string,int>P1("张三",18);
	P1.showPerson();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：类模板和函数模板语法相似，在声明模板template后面加类，此类称为类模板





#### 1.3.2类模板与函数模板的区别

类模板与函数模板区别主要有两点：

1. 类模板没有自动类型推导的使用方式
2. 类模板在模板参数列表中可以有默认参数



示例：

```c++
#include <string>
//类模板
template<class NameType, class AgeType = int> 
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->mName = name;
		this->mAge = age;
	}
	void showPerson()
	{
		cout << "name: " << this->mName << " age: " << this->mAge << endl;
	}
public:
	NameType mName;
	AgeType mAge;
};

//1、类模板没有自动类型推导的使用方式
void test01()
{
	// Person p("孙悟空", 1000); // 错误 类模板使用时候，不可以用自动类型推导
	Person <string ,int>p("孙悟空", 1000); //必须使用显示指定类型的方式，使用类模板
	p.showPerson();
}

//2、类模板在模板参数列表中可以有默认参数
void test02()
{
	Person <string> p("猪八戒", 999); //类模板中的模板参数列表 可以指定默认参数
	p.showPerson();
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

总结：

* 类模板使用只能用显示指定类型方式
* 类模板中的模板参数列表可以有默认参数





#### 1.3.3类模板中成员函数创建时机



类模板中成员函数和普通类中成员函数创建时机是有区别的：

* 普通类中的成员函数一开始就可以创建
* 类模板中的成员函数在调用时才创建



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

class Person1
{
public:
	void showPerson1()
	{
		cout << "Person1 show" << endl;
	}

};

class Person2
{
public:
	void showPerson2()
	{
		cout << "Person2 show" << endl;
	}

};

template<class T>
class MyClass
{
public:
	T obj;
	//类模板中的成员函数，并不是一开始就创建的，而是在模板调用时再生成
	void func1() { obj.showPerson1(); }
	void func2() { obj.showPerson2(); }

};


void test01()
{
	MyClass<Person1> m;
	m.func1();
	//m.func2();//编译会出错，说明函数调用才会去创建成员函数
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：类模板中的成员函数并不是一开始就创建的，在调用时才去创建



#### 1.3.4类模板对象做函数参数



学习目标：

* 类模板实例化出的对象，向函数传参的方式



一共有三种传入方式：

1. 指定传入的类型   --- 直接显示对象的数据类型
2. 参数模板化           --- 将对象中的参数变为模板进行传递
3. 整个类模板化       --- 将这个对象类型 模板化进行传递



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

template<class NameType,class AgeType=int>
class Person
{
public:
	Person(NameType name, AgeType age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
	void showPerson()
	{
		cout << "name: " << this->m_Name << " age: " << this->m_Age << endl;
	}
public:
	NameType m_Name;
	AgeType m_Age;
};

//1.指定传入的类型
void printPerson1(Person<string,int>& p)
{
	p.showPerson();
}

void test01()
{
	Person<string,int>P1("孙悟空", 100);
	printPerson1(P1);
}


//2.参数模板化
template<class T1,class T2>
void printPerson2(Person<T1, T2>& p)
{
	p.showPerson();
	cout << "T1的类型为：" << typeid(T1).name() << endl;
	cout << "T1的类型为：" << typeid(T2).name() << endl;
}

void test02()
{
	Person<string, int>P2("猪八戒", 90);
	printPerson2(P2);
}

//整个类模板化
template<class T>
void printPerson3(T& p)
{
	p.showPerson();
	cout << "T的类型为：" << typeid(T).name() << endl;
}

void test03()
{
	Person<string, int>P3("唐僧", 80);
	printPerson3(P3);
}

int main()
{
	test01();
	test02();
	test03();
	system("pause");
	return 0;
}
```

总结：

* 通过类模板创建的对象，可以有三种方式向函数中进行传参
* 使用比较广泛是第一种：指定传入的类型



若想知道所用模板是什么数据类型，可借用以下语句查看：

```c++
cout << "T的类型为：" << typeid(T).name() << endl;
```





#### 1.3.5类模板与继承

当类模板碰到继承时，需要注意一下几点：

* 当子类继承的父类是一个类模板时，子类在声明的时候，要指定出父类中T的类型
* 如果不指定，编译器无法给子类分配内存
* 如果想灵活指定出父类中T的类型，子类也需变为类模板



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

template<class T>
class Base
{
	T m;
};

//class Son :public Bass //错误，C++编译需要给子类分配内存，必须知道父类中T的类型才可以向下继承
class Son:public Base<int>	//必须指定一个类型
{

};

void test01()
{
	Son c;
}

//类模板继承类模板，可以用T2指定父类中的T类型
template<class T1,class T2>
class Son2 :public Base<T2>
{
public:
	Son2()
	{
		cout << typeid(T1).name() << endl;	//int
		cout << typeid(T2).name() << endl;	//char
	}
};

void test02()
{
	Son2<int, char>child1;
}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```

总结：如果父类是类模板，子类需要指定出父类中T的数据类型





#### 1.3.6类模板成员函数类外实现

学习目标：能够掌握类模板中的成员函数类外实现



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

//类模板中成员函数类外实现
template<class T1,class T2>
class Person
{
public:
	//成员函数类内声明
	Person(T1 name, T2 age);
	void showPerson();
public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数，类外实现
template<class T1,class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
	this->m_Name = name;
	this->m_Age = age;
}

template<class T1,class T2>
void Person<T1, T2>::showPerson()
{
	cout << "name: " << this->m_Name << " age: " << this->m_Age << endl;
}


void test01()
{
	Person<string, int>p("Tom", 20);
	p.showPerson();
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：类模板中成员函数类外实现时，需要加上模板参数列表





#### 1.3.7类模板分文件编写



学习目标：

* 掌握类模板成员函数分文件编写产生的问题以及解决方式

问题：

* 类模板中成员函数创建时机是在调用阶段，导致分文件编写时链接不到


解决：

* 解决方式1：直接包含.cpp源文件
* 解决方式2：将声明和实现写到同一个文件中，并更改后缀名为.hpp，hpp是约定的名称，并不是强制



示例：

person.hpp中代码：

```c++
#pragma once
#include <iostream>
using namespace std;
#include <string>

template<class T1, class T2>
class Person 
{
public:
	Person(T1 name, T2 age);
	void showPerson();
public:
	T1 m_Name;
	T2 m_Age;
};

//构造函数 类外实现
template<class T1, class T2>
Person<T1, T2>::Person(T1 name, T2 age)
{
	this->m_Name = name;
	this->m_Age = age;
}

//成员函数 类外实现
template<class T1, class T2>
void Person<T1, T2>::showPerson() 
{
	cout << "姓名: " << this->m_Name << " 年龄:" << this->m_Age << endl;
}
```



类模板分文件编写.cpp中代码

```c++
#include<iostream>
using namespace std;

//#include "person.h"
#include "person.cpp" //解决方式1，包含cpp源文件

//解决方式2，将声明和实现写到一起，文件后缀名改为.hpp
#include "person.hpp"
void test01()
{
	Person<string, int> p("Tom", 10);
	p.showPerson();
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：主流的解决方式是第二种，将类模板成员函数写到一起，并将后缀名改为.hpp





#### 1.3.8类模板与友元



学习目标：

* 掌握类模板配合友元函数的类内和类外实现



全局函数类内实现 - 直接在类内声明友元即可

全局函数类外实现 - 需要提前让编译器知道全局函数的存在



全局函数类内实现：

```c++
#include <iostream>
#include <string>

using namespace std;

template<class T1,class T2>
class Person
{
public:
	//1.全局函数配合友元 类内实现
	friend void printPerson1(Person<T1, T2>& p)
	{
		cout << "类内实现---姓名：" << p.m_Name << " 年纪：" << p.m_Age << endl;
	}
public:
	Person(T1 name, T2 age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
private:
	T1 m_Name;
	T2 m_Age;
};

//1.全局函数在类内实现
void test01()
{
	Person<string, int>P("Tom", 18);
	printPerson1(P);
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



全局函数类外实现：

```c++
#include <iostream>
#include <string>

using namespace std;
//首先让编译器知道有Person类的模板声明
template<class T1,class T2>
class Person;

//再让编译器知道有printPerson2()这个函数声明
template<class T1,class T2>
void printPerson2(Person<T1, T2>& p);

template<class T1,class T2>
class Person
{
public:
	//2.全局函数配合友元 类外实现
	friend void printPerson2<>(Person<T1, T2>& p);	//注意要加<>号才能实现

public:
	Person(T1 name, T2 age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}
private:
	T1 m_Name;
	T2 m_Age;
};

template<class T1,class T2>
void printPerson2(Person<T1, T2>& p)
{
	cout << "类外实现---姓名：" << p.m_Name << " 年纪：" << p.m_Age << endl;
}

//2.全局函数在类外实现
void test02()
{
	Person<string, int>P("Jerry", 18);
	printPerson2(P);
}

int main()
{
	test02();
	system("pause");
	return 0;
}
```



总结：建议全局函数做类内实现，用法简单，而且编译器可以直接识别





#### 1.3.9类模板案例



案例描述:  实现一个通用的数组类，要求如下：



* 可以对内置数据类型以及自定义数据类型的数据进行存储
* 将数组中的数据存储到堆区
* 构造函数中可以传入数组的容量
* 提供对应的拷贝构造函数以及operator=防止浅拷贝问题
* 提供尾插法和尾删法对数组中的数据进行增加和删除
* 可以通过下标的方式访问数组中的元素
* 可以获取数组中当前元素个数和数组的容量





示例：

```c++

```









## 2.STL初始识

### 2.1 STL的诞生



* 长久以来，软件界一直希望建立一种可重复利用的东西

* C++的**面向对象**和**泛型编程**思想，目的就是**复用性的提升**

* 大多情况下，数据结构和算法都未能有一套标准,导致被迫从事大量重复工作

* 为了建立数据结构和算法的一套标准,诞生了**STL**

  


### 2.2 STL基本概念



* STL(Standard Template Library,**标准模板库**)
* STL 从广义上分为: **容器(container) 算法(algorithm) 迭代器(iterator)**
* **容器**和**算法**之间通过**迭代器**进行无缝连接。
* STL 几乎所有的代码都采用了模板类或者模板函数



### 2.3 STL六大组件

STL大体分为六大组件，分别是:**容器、算法、迭代器、仿函数、适配器（配接器）、空间配置器**



1. 容器：各种数据结构，如vector、list、deque、set、map等,用来存放数据。
2. 算法：各种常用的算法，如sort、find、copy、for_each等
3. 迭代器：扮演了容器与算法之间的胶合剂。
4. 仿函数：行为类似函数，可作为算法的某种策略。
5. 适配器：一种用来修饰容器或者仿函数或迭代器接口的东西。
6. 空间配置器：负责空间的配置与管理。



### 2.4  STL中容器、算法、迭代器



**容器：**置物之所也

STL**容器**就是将运用**最广泛的一些数据结构**实现出来

常用的数据结构：数组, 链表,树, 栈, 队列, 集合, 映射表 等

这些容器分为**序列式容器**和**关联式容器**两种:

​	**序列式容器**:强调值的排序，序列式容器中的每个元素均有固定的位置。
​	**关联式容器**:二叉树结构，各元素之间没有严格的物理上的顺序关系



**算法：**问题之解法也

有限的步骤，解决逻辑或数学上的问题，这一门学科我们叫做算法(Algorithms)

算法分为:**质变算法**和**非质变算法**。

质变算法：是指运算过程中会更改区间内的元素的内容。例如拷贝，替换，删除等等

非质变算法：是指运算过程中不会更改区间内的元素内容，例如查找、计数、遍历、寻找极值等等



**迭代器：**容器和算法之间粘合剂

提供一种方法，使之能够依序寻访某个容器所含的各个元素，而又无需暴露该容器的内部表示方式。

每个容器都有自己专属的迭代器

迭代器使用非常类似于指针，初学阶段我们可以先理解迭代器为指针



迭代器种类：

| 种类           | 功能                                                     | 支持运算                                |
| -------------- | -------------------------------------------------------- | --------------------------------------- |
| 输入迭代器     | 对数据的只读访问                                         | 只读，支持++、==、！=                   |
| 输出迭代器     | 对数据的只写访问                                         | 只写，支持++                            |
| 前向迭代器     | 读写操作，并能向前推进迭代器                             | 读写，支持++、==、！=                   |
| 双向迭代器     | 读写操作，并能向前和向后操作                             | 读写，支持++、--，                      |
| 随机访问迭代器 | 读写操作，可以以跳跃的方式访问任意数据，功能最强的迭代器 | 读写，支持++、--、[n]、-n、<、<=、>、>= |

常用的容器中迭代器种类为双向迭代器，和随机访问迭代器





### 2.5容器算法迭代器初识



了解STL中容器、算法、迭代器概念之后，我们利用代码感受STL的魅力

STL中最常用的容器为Vector，可以理解为数组，下面我们将学习如何向这个容器中插入数据、并遍历这个容器



#### 2.5.1vector存放内置数据类型

容器：     `vector`

算法：     `for_each`

迭代器： `vector<int>::iterator`



示例：

```c++
#include <iostream>
#include <algorithm>
#include <vector>

using namespace std;

void Myprint(int val)
{
	cout << val << endl;
}

void test01()
{
	//创建vector容器对象，并且通过模板参数指定容器中存放的数据类型
	vector<int> v;
	//向容器中放数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	//每一个容器都有自己的迭代器，迭代器是用来遍历容器中的元素
	//v.begin()返回迭代器，这个迭代器指向容器中第一个数据
	//v.end()返回迭代器，这个迭代器指向容器元素的最后一个元素的下一个位置
	//vector<int>::iterator 拿到vector<int>这种容器的迭代器类型

	vector<int>::iterator pBegin = v.begin();
	vector<int>::iterator pEnd = v.end();

	//第一种遍历方式
	cout << "第一种遍历方式：" << endl;
	cout << "-----------------" << endl;
	while (pBegin != pEnd)
	{		cout << *pBegin << endl;
		pBegin++;
	}
	cout << "-----------------" << endl;
}

void test02()
{
	//创建vector容器对象，并且通过模板参数指定容器中存放的数据类型
	vector<int> v;
	//向容器中放数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	vector<int>::iterator pBegin = v.begin();
	vector<int>::iterator pEnd = v.end();

	//第二种遍历方式
	cout << "第二种遍历方式：" << endl;
	cout << "-----------------" << endl;
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
	{
		cout << *it << endl;
	}
	cout << "-----------------" << endl;

}

void test03()
{
	//创建vector容器对象，并且通过模板参数指定容器中存放的数据类型
	vector<int> v;
	//向容器中放数据
	v.push_back(10);
	v.push_back(20);
	v.push_back(30);
	v.push_back(40);

	vector<int>::iterator pBegin = v.begin();
	vector<int>::iterator pEnd = v.end();

	//第三种遍历方式，使用STL提供的标准遍历算法,for_each()算法中需要输入，首指针，未指针，对应输出函数
	cout << "第三种遍历方式：" << endl;
	cout << "-----------------" << endl;
	for_each(v.begin(), v.end(), Myprint);
	cout << "-----------------" << endl;
}

int main()
{
	test01();
	test02();
	test03();
	system("pause");
	return 0;
}
```



#### 2.5.2vector存放自定义数据类型

学习目标：vector中存放自定义数据类型，并打印输出



示例:

```c++
#include <iostream>
#include <vector>
#include <string>

using namespace std;

//自定义数据类型
class Person
{
public:
	Person(string name, int age)
	{
		this->m_Name = name;
		this->m_Age = age;
	}

public:
	string m_Name;
	int m_Age;
};

//存放对象
void test01()
{
	vector<Person> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);

	v.push_back(p1);
	v.push_back(p2);
	v.push_back(p3);
	v.push_back(p4);
	v.push_back(p5);

	for (vector<Person>::iterator it = v.begin(); it < v.end(); it++)
	{
		cout << "name: " << it->m_Name << " age: " << it->m_Age << endl;
	}

}

//放对象指针
void test02()
{
	vector<Person*> v;

	//创建数据
	Person p1("aaa", 10);
	Person p2("bbb", 20);
	Person p3("ccc", 30);
	Person p4("ddd", 40);
	Person p5("eee", 50);

	v.push_back(&p1);
	v.push_back(&p2);
	v.push_back(&p3);
	v.push_back(&p4);
	v.push_back(&p5);

	for (vector<Person*>::iterator it = v.begin(); it < v.end(); it++)
	{
		cout << "name: " << (*it)->m_Name << " age: " << (*it)->m_Age << endl;
	}

}

int main()
{
	test01();
	test02();
	system("pause");
	return 0;
}
```



==*it就是<>中的数据类型==



#### 2.5.3vector容器嵌套容器

学习目标：容器中嵌套容器，我们将所有数据进行遍历输出



示例：

```c++
#include <iostream>
#include <vector>

using namespace std;

//容器嵌套容器
void test01()
{
	vector<vector<int>> v;
	
	vector<int> v1;
	vector<int> v2;
	vector<int> v3;
	vector<int> v4;

	for (int i = 0; i < 4; i++)
	{
		v1.push_back(i + 1);
		v2.push_back(i + 2);
		v3.push_back(i + 3);
		v4.push_back(i + 4);
	}

	//将容器元素插入到vector v中
	v.push_back(v1);
	v.push_back(v2);
	v.push_back(v3);
	v.push_back(v4);

	for (vector<vector<int>>::iterator it = v.begin(); it != v.end(); it++)
	{
		for (vector<int>::iterator vit = (*it).begin(); vit != (*it).end(); vit++)
		{
			cout << *vit << " ";
		}
		cout << endl;
	}

}

int main()
{
	test01();
	system("pause");
	return 0;
}
```





## 3.STL-常用容器



### 3.1string容器

#### 3.1.1 string基本概念

**本质：**

* string是C++风格的字符串，而string本质上是一个类



**string和char * 区别：**

* char * 是一个指针
* string是一个类，类内部封装了char\*，管理这个字符串，是一个char*型的容器。



**特点：**

string 类内部封装了很多成员方法

例如：查找find，拷贝copy，删除delete 替换replace，插入insert

string管理char*所分配的内存，不用担心复制越界和取值越界等，由类内部进行负责



#### 3.1.2 string构造函数

构造函数原型：

* `string();`          				//创建一个空的字符串 例如: string str;
  `string(const char* s);`	        //使用字符串s初始化
* `string(const string& str);`    //使用一个string对象初始化另一个string对象
* `string(int n, char c);`           //使用n个字符c初始化 



示例：

```c++
#include <iostream>
#include <string>

using namespace std;

/*
* `string();`          				//创建一个空的字符串 例如: string str;
  `string(const char* s);`	        //使用字符串s初始化
* `string(const string& str);`    //使用一个string对象初始化另一个string对象
* `string(int n, char c);`           //使用n个字符c初始化
*/

void test01()
{
	string s1;//无参构造
	cout << "str1=" << s1 << endl;

	const char* str = "hello world";
	string s2(str);	//使用字符串s初始化
	cout << "str2= " << s2 << endl;

	string s3(s2);
	cout << "str3= " << s3 << endl;

	string s4(10,'a');
	cout << "str4= " << s4 << endl;

}


int main()
{
	test01();
	system("pause");
	return 0;
}
```



#### 3.1.3string赋值操作



功能描述：

* 给string字符串进行赋值



赋值的函数原型：

* `string& operator=(const char* s);`             //char*类型字符串 赋值给当前的字符串
* `string& operator=(const string &s);`         //把字符串s赋给当前的字符串
* `string& operator=(char c);`                          //字符赋值给当前的字符串
* `string& assign(const char *s);`                  //把字符串s赋给当前的字符串
* `string& assign(const char *s, int n);`     //把字符串s的前n个字符赋给当前的字符串
* `string& assign(const string &s);`              //把字符串s赋给当前字符串
* `string& assign(int n, char c);`                  //用n个字符c赋给当前字符串



示例：

```c++
//赋值
void test01()
{
	string str1;
	str1 = "hello world";
	cout << "str1 = " << str1 << endl;

	string str2;
	str2 = str1;
	cout << "str2 = " << str2 << endl;

	string str3;
	str3 = 'a';
	cout << "str3 = " << str3 << endl;

	string str4;
	str4.assign("hello c++");
	cout << "str4 = " << str4 << endl;

	string str5;
	str5.assign("hello c++",5);
	cout << "str5 = " << str5 << endl;


	string str6;
	str6.assign(str5);
	cout << "str6 = " << str6 << endl;

	string str7;
	str7.assign(5, 'x');
	cout << "str7 = " << str7 << endl;
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：

​	string的赋值方式很多，`operator=`  这种方式是比较实用的



#### 3.1.4string字符串拼接

**功能描述：**

* 实现在字符串末尾拼接字符串



**函数原型：**

* `string& operator+=(const char* str);`                   //重载+=操作符
* `string& operator+=(const char c);`                         //重载+=操作符
* `string& operator+=(const string& str);`                //重载+=操作符
* `string& append(const char *s); `                               //把字符串s连接到当前字符串结尾
* `string& append(const char *s, int n);`                 //把字符串s的前n个字符连接到当前字符串结尾
* `string& append(const string &s);`                           //同operator+=(const string& str)
* `string& append(const string &s, int pos, int n);`//字符串s中从pos开始的n个字符连接到字符串结尾



示例：

```c++
//字符串拼接
void test01()
{
	string str1 = "我";
	str1 += "爱玩游戏";
	cout << "str1 = " << str1 << endl;	//输出：我爱玩游戏
    
	str1 += ':';
	cout << "str1 = " << str1 << endl;	//输出：我爱玩游戏：
    
	string str2 = "LOL DNF";
	str1 += str2;
	cout << "str1 = " << str1 << endl;	//输出：我爱玩游戏：LOL DNF

	string str3 = "I";
	str3.append(" love ");	//str3=I love 
	str3.append("game abcde", 4);	//str3=I love game
	//str3.append(str2);
	str3.append(str2, 4, 3); // 从下标4位置开始 ，截取3个字符，拼接到字符串末尾
	cout << "str3 = " << str3 << endl;	//输出：str3 = I love gameDNF
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```



总结：字符串拼接的重载版本很多，初学阶段记住几种即可



#### 3.1.5string查找和替换

**功能描述：**

* 查找：查找指定字符串是否存在
* 替换：在指定的位置替换字符串



**函数原型：**

* `int find(const string& str, int pos = 0) const;`              //查找str第一次出现位置,从pos开始查找
* `int find(const char* s, int pos = 0) const; `                     //查找s第一次出现位置,从pos开始查找
* `int find(const char* s, int pos, int n) const; `               //从pos位置查找s的前n个字符第一次位置
* `int find(const char c, int pos = 0) const; `                       //查找字符c第一次出现位置
* `int rfind(const string& str, int pos = npos) const;`      //查找str最后一次位置,从pos开始查找
* `int rfind(const char* s, int pos = npos) const;`              //查找s最后一次出现位置,从pos开始查找
* `int rfind(const char* s, int pos, int n) const;`              //从pos查找s的前n个字符最后一次位置
* `int rfind(const char c, int pos = 0) const;  `                      //查找字符c最后一次出现位置
* `string& replace(int pos, int n, const string& str); `       //替换从pos开始n个字符为字符串str
* `string& replace(int pos, int n,const char* s); `                 //替换从pos开始的n个字符为字符串s





示例：

```c++
//查找和替换
void test01()
{
	//查找
	string str1 = "abcdefgde";
	int pos = str1.find("de");	//若未找到则返回-1
	if (pos == -1)
	{
		cout << "未找到" << endl;	
	}
	else
	{
		cout << "pos = " << pos << endl;	//输出3，首位是0
	}
	
	pos = str1.rfind("de");
	cout << "pos = " << pos << endl;	//输出7，首位是0

}

void test02()
{
	//替换
	string str1 = "abcdefgde";
	str1.replace(1, 3, "1111");
	//从1号位置起 3个字符替换为“1111”
	cout << "str1 = " << str1 << endl;	//输出a1111efgde
}

int main() 
{

	//test01();
	//test02();
	system("pause");
	return 0;
}
```

总结：

* find查找是从左往后，rfind从右往左
* find找到字符串后返回查找的第一个字符位置，找不到返回-1
* replace在替换时，要指定从哪个位置起，多少个字符，替换成什么样的字符串





#### 3.1.6string字符串比较

**功能描述：**

* 字符串之间的比较

**比较方式：**

* 字符串比较是按字符的ASCII码进行对比

= 返回   0

\> 返回   1 

< 返回  -1



**函数原型：**

* `int compare(const string &s) const; `  //与字符串s比较
* `int compare(const char *s) const;`      //与字符串s比较



示例：

```c++
//字符串比较
void test01()
{

	string s1 = "hello";
	string s2 = "aello";

	int ret = s1.compare(s2);

	if (ret == 0) {
		cout << "s1 等于 s2" << endl;
	}
	else if (ret > 0)
	{
		cout << "s1 大于 s2" << endl;
	}
	else
	{
		cout << "s1 小于 s2" << endl;
	}

}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：字符串对比主要是用于比较两个字符串是否相等，判断谁大谁小的意义并不是很大





#### 3.1.7string字符存取



string中单个字符存取方式有两种

* `char& operator[](int n); `     //通过[]方式取字符
* `char& at(int n);   `                    //通过at方法获取字符



示例：

```c++
void test01()
{
	string str = "hello world";
	
    //1.通过[]来访问字符，str.size()可以获得字符串长度
	for (int i = 0; i < str.size(); i++)
	{
		cout << str[i] << " ";
	}
	cout << endl;
	
    //2.通过at方式访问单个字符
	for (int i = 0; i < str.size(); i++)
	{
		cout << str.at(i) << " ";
	}
	cout << endl;

	//字符修改
	str[0] = 'x';	//str=xello world
	str.at(1) = 'x';	//str=xxllo world
	cout << str << endl;
	
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：string字符串中单个字符存取有两种方式，利用 [ ] 或 at





#### 3.1.8string插入和删除

**功能描述：**

* 对string字符串进行插入和删除字符操作

**函数原型：**

* `string& insert(int pos, const char* s);  `                //插入字符串
* `string& insert(int pos, const string& str); `        //插入字符串
* `string& insert(int pos, int n, char c);`                //在指定位置插入n个字符c
* `string& erase(int pos, int n = npos);`                    //删除从Pos开始的n个字符 



示例：

```c++
//字符串插入和删除
void test01()
{
	string str = "hello";
	str.insert(1, "111");
	cout << str << endl;	/str=h111ello

	str.erase(1, 3);  //从1号位置开始3个字符
	cout << str << endl;	//str=hello
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

**总结：**插入和删除的起始下标都是从0开始



#### 3.1.9string子串

**功能描述：**

* 从字符串中获取想要的子串

**函数原型：**

* `string substr(int pos = 0, int n = npos) const;`   //返回由pos开始的n个字符组成的字符串



示例：

```c++
//子串
void test01()
{

	string str = "abcdefg";
	string subStr = str.substr(1, 3);
	cout << "subStr = " << subStr << endl;	//subStr=bcd

	string email = "hello@sina.com";
    //从邮件地址中获取用户名信息
	int pos = email.find("@");	//pos=5
	string username = email.substr(0, pos);	//截取用户名
	cout << "username: " << username << endl;

}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

**总结：**灵活的运用求子串功能，可以在实际开发中获取有效的信息





### 3.2vector容器



#### 3.2.1vector基本概念

**功能：**

* vector数据结构和**数组非常相似**，也称为**单端数组**

**vector与普通数组区别：**

* 不同之处在于数组是静态空间，而vector可以**动态扩展**

**动态扩展：**

* 并不是在原空间之后续接新空间，而是找更大的内存空间，然后将原数据拷贝新空间，释放原空间



![说明: 2015-11-10_151152](D:/计算机自学/C++/黑马程序员/原文件/匠心精作C++从0到1入门编程-学习编程不再难资料/第5阶段-C++提高编程资料/讲义/assets/clip_image002.jpg)



* vector容器的迭代器是支持随机访问的迭代器

#### 3.2.2 vector构造函数

**功能描述：**

* 创建vector容器



**函数原型：**

* `vector<T> v; `               		     //采用模板实现类实现，默认构造函数
* `vector(v.begin(), v.end());   `       //将v[begin(), end())区间中的元素拷贝给本身。
* `vector(n, elem);`                            //构造函数将n个elem拷贝给本身。
* `vector(const vector &vec);`         //拷贝构造函数。



示例：

```c++
#include <vector>

//打印容器接口
void printVector(vector<int>& v)
{
	for (vector<int>::iterator it = v.begin(); it != v.end(); it++)
    {
		cout << *it << " ";
	}
	cout << endl;
}

void test01()
{
	vector<int> v1; //无参构造（默认构造）
    
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	printVector(v1);	//输出容器数据
	
    //2.通过区间方式进行构造
	vector<int> v2(v1.begin(), v1.end());
	printVector(v2);

    //3.n个elem方式构造，赋值10个100
	vector<int> v3(10, 100);
	printVector(v3);
	
    //4.拷贝构造
	vector<int> v4(v3);
	printVector(v4);
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

**总结：**vector的多种构造方式没有可比性，灵活使用即可



#### 3.2.3 vector赋值操作



**功能描述：**

* 给vector容器进行赋值



**函数原型：**

* `vector& operator=(const vector &vec);`//重载等号操作符


* `assign(beg, end);`       //将[beg, end)区间中的数据拷贝赋值给本身。
* `assign(n, elem);`        //将n个elem拷贝赋值给本身。

**示例：**

```C++
#include <vector>

//打印输出函数
void printVector(vector<int>& v)
{

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) 
    {
		cout << *it << " ";
	}
	cout << endl;
}

//赋值操作
void test01()
{
    
	vector<int> v1; //无参构造
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	printVector(v1);
	
    //1.=赋值操作
	vector<int>v2;
	v2 = v1;
	printVector(v2);
	
    //2.assign赋值操作,前闭后开
	vector<int>v3;
	v3.assign(v1.begin(), v1.end());
	printVector(v3);
	
    //3.assign赋值操作，将n个elem赋值进v4
	vector<int>v4;
	v4.assign(10, 100);
	printVector(v4);
}

int main() 
{
	test01();
	system("pause");
	return 0;
}

```

总结： vector赋值方式比较简单，使用operator=，或者assign都可以



#### 3.2.4  vector容量和大小

**功能描述：**

* 对vector容器的容量和大小操作



**函数原型：**

* `empty(); `                            //判断容器是否为空

* `capacity();`                      //容器的容量

* `size();`                              //返回容器中元素的个数

* `resize(int num);`             //重新指定容器的长度为num，若容器变长，则以默认值填充新位置。

  ​					      //如果容器变短，则末尾超出容器长度的元素被删除。

* `resize(int num, elem);`  //重新指定容器的长度为num，若容器变长，则以elem值填充新位置。

  ​				              //如果容器变短，则末尾超出容器长度的元素被删除




**示例：**


```C++
#include <vector>

//打印输出函数
void printVector(vector<int>& v)
{

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) {
		cout << *it << " ";
	}
	cout << endl;
}

void test01()
{
	vector<int> v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	printVector(v1);
    
	if (v1.empty())	//为真 代表容器为空
	{
		cout << "v1为空" << endl;
	}
	else
	{
		cout << "v1不为空" << endl;
		cout << "v1的容量 = " << v1.capacity() << endl;	//容量被系统扩展到13
		cout << "v1的大小 = " << v1.size() << endl;		//大小为10；
	}

	//resize 重新指定大小 ，若指定的更大，默认用0填充新位置，可以利用重载版本替换默认填充
	v1.resize(15,10);
	printVector(v1);	

	//resize 重新指定大小 ，若指定的更小，超出部分元素被删除
	v1.resize(5);
	printVector(v1);	//输出01234
}

int main()
{
	test01();
	system("pause");
	return 0;
}

```

总结：

* 判断是否为空  --- empty
* 返回元素个数  --- size
* 返回容器容量  --- capacity
* 重新指定大小  ---  resize





#### 3.2.5 vector插入和删除

**功能描述：**

* 对vector容器进行插入、删除操作



**函数原型：**

* `push_back(ele);`                                         //尾部插入元素ele
* `pop_back();`                                                //删除最后一个元素
* `insert(const_iterator pos, ele);`        //迭代器指向位置pos插入元素ele
* `insert(const_iterator pos, int count,ele);`//迭代器指向位置pos插入count个元素ele
* `erase(const_iterator pos);`                     //删除迭代器指向的元素
* `erase(const_iterator start, const_iterator end);`//删除迭代器从start到end之间的元素
* `clear();`                                                        //删除容器中所有元素





**示例：**

```C++
#include <vector>

//打印输出函数
void printVector(vector<int>& v) 
{

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) 
    {
		cout << *it << " ";
	}
	cout << endl;
}

//插入和删除
void test01()
{
	vector<int> v1;
	//尾插
	v1.push_back(10);
	v1.push_back(20);
	v1.push_back(30);
	v1.push_back(40);
	v1.push_back(50);
	printVector(v1);	//输出10 20 30 40 50
    
	//尾删
	v1.pop_back();
	printVector(v1);	//输出10 20 30 40
    
	//插入
	v1.insert(v1.begin(), 100);
	printVector(v1);	//输出100 10 20 30 40

	v1.insert(v1.begin(), 2, 1000);
	printVector(v1);	//输出1000 1000 100 10 20 30 40

	//删除
	v1.erase(v1.begin());
	printVector(v1);	//输出1000 100 10 20 30 40

	//清空
	v1.erase(v1.begin(), v1.end());
	v1.clear();
	printVector(v1);	//输出为空
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：

* 尾插  --- push_back
* 尾删  --- pop_back
* 插入  --- insert    (位置迭代器)
* 删除  --- erase  （位置迭代器）
* 清空  ---  clear  



#### 3.2.6 vector数据存取



**功能描述：**

* 对vector中的数据的存取操作



**函数原型：**

* `at(int idx); `     //返回索引idx所指的数据
* `operator[]; `       //返回索引idx所指的数据
* `front(); `            //返回容器中第一个数据元素
* `back();`              //返回容器中最后一个数据元素



**示例：**

```C++
#include <vector>

void test01()
{
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	
    //打印输出数组中的元素，打印0~9
	for (int i = 0; i < v1.size(); i++)
	{
		cout << v1[i] << " ";
	}
	cout << endl;
	
    //利用成员函数at访问元素，打印0~9
	for (int i = 0; i < v1.size(); i++)
	{
		cout << v1.at(i) << " ";
	}
	cout << endl;

	cout << "v1的第一个元素为： " << v1.front() << endl;
	cout << "v1的最后一个元素为： " << v1.back() << endl;
}

int main()
{
	test01();
	system("pause");
	return 0;
}
```

总结：

* 除了用迭代器获取vector容器中元素，[ ]和at也可以
* front返回容器第一个元素
* back返回容器最后一个元素



#### 3.2.7 vector互换容器

**功能描述：**

* 实现两个容器内元素进行互换

**函数原型：**

* `swap(vec);`  // 将vec与本身的元素互换

**示例：**

```C++
#include <vector>

//打印输出函数
void printVector(vector<int>& v) 
{

	for (vector<int>::iterator it = v.begin(); it != v.end(); it++) 
    {
		cout << *it << " ";
	}
	cout << endl;
}

void test01()
{
	vector<int>v1;
	for (int i = 0; i < 10; i++)
	{
		v1.push_back(i);
	}
	printVector(v1);	//打印输出v1的元素0~9

	vector<int>v2;
	for (int i = 10; i > 0; i--)
	{
		v2.push_back(i);
	}
	printVector(v2);	//打印输出v2的元素10~1

	//互换容器
	cout << "互换后" << endl;
	v1.swap(v2);	//将容器v1和容器v2互换
	printVector(v1);
	printVector(v2);
}

//实际用途
void test02()
{
	vector<int> v;
	for (int i = 0; i < 100000; i++) 
    {
		v.push_back(i);
	}

	cout << "v的容量为：" << v.capacity() << endl;	//138255
	cout << "v的大小为：" << v.size() << endl;		//100000

	v.resize(3);	//重新指定大小

	cout << "v的容量为：" << v.capacity() << endl;	//138255
	cout << "v的大小为：" << v.size() << endl;		//3

	//收缩内存
	vector<int>(v).swap(v); //匿名对象,系统直接将匿名对象回收

	cout << "v的容量为：" << v.capacity() << endl;	//3
	cout << "v的大小为：" << v.size() << endl;		//3
}

int main() 
{
	test01();
	test02();
	system("pause");
	return 0;
}

```

总结：swap可以使两个容器互换，可以达到实用的收缩内存效果



#### 3.2.8 vector预留空间

**功能描述：**

* 减少vector在动态扩展容量时的扩展次数

**函数原型：**

* `reserve(int len);`//容器预留len个元素长度，预留位置不初始化，元素不可访问。

**示例：**

```C++
#include <vector>

void test01()
{
	vector<int> v;
	//预留空间
	v.reserve(100000);
	int num = 0;	//统计开辟次数
	int* p = NULL;	
	for (int i = 0; i < 100000; i++) 
    {
		v.push_back(i);
		if (p != &v[0]) 
        {
			p = &v[0];
			num++;
		}
	}
	cout << "num:" << num << endl;	//如果没有预留空间则输出内存开辟的次数，如果预留了空间则只开辟1次
}

int main() 
{
	test01();
	system("pause");
	return 0;
}
```

总结：如果数据量较大，可以一开始利用reserve预留空间
