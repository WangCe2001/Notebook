



# 第3章处理数据

## 3.1 简单变量

1.C++的命名规则：

在名称中只能使用**字母**字符、**数字**和**下划线(_)**

名称的第一个字符不能是数字

区分大写字符与小写字符

不能用C++的关键字作名称

2.sizeof运算符返回类型或变量的长度，单位为字节

3.unsigned本身是unsigned int 的缩写



## 3.2 const限定符

1.C++中也可以使用#define来定义常量，但是const比#define要更好



## 3.3 浮点数

1.d.ddde+n指的是将小数点向右移n位，d.ddde-n指的是将小数点向左移n位

例如：3.14e+4=31400，3.14e-4=0.000314

2.double类型至少有==13位是精确==的，float类型C++只保证==6位有效位==。

3.在==默认的情况下，浮点常量都属于double==类型。

4.如果希望常量是float类型，请使用f或F后缀

5.如果想使用 long double类型，可使用l或L后缀，(由于小写l像1，所以使用L是更好的选择) 



## 3.4 C++算术运算符

1.使用%求模运算符号时，两个数字必须是整型，将该运算符用于浮点数将导致编译错误

2.使用/除法符号时，如果两个数是整型，那么运算结果的小数部分将会被遗弃，最后得到的结果将会是一个整数

3.强制类型转换有以下形式：

```c++
(typename) value;
typename (value);
//例子如下：
(int) 数值;
int (数值);
```

# 第4章 复合类型

## 4.1 数组

1.定义数组的一般表达式：

```c++
typename arrayName[arraySize];
//arraySize不可以是变量，必须在编译前已知
```

2.sizeof运算符用于数组名，得到的将是整个数组中的字节数；如果将sizeof用于数组元素，则得到的将是元素的长度(单位为字节)

```c++
int arr[4]={1,2,3,4};
int arr[]={1,2,3,4};
//这两条语句效果一样
sizeof(arr)==16;
sizeof(arr[0])==4;
```

3.如果只对数组的一部分进行初始化，则编译器将把其他元素设置为0

```c++
int arr[4]={1};	//编译时四个元素分别为1，0，0，0
//如果想对数组中的所有元素都初始化为0，可以如下操作
int arr[5]={0};	//所有元素编译时将会被初始化为0
```

## 4.2 字符串

1.C风格的字符串具有一种特殊的性质：以==空字符"\0"为结尾==，其ASCII码为0，用来标记字符串的结尾

```c++
char dog[8] = {'b','e','a','u','x',' ','I','I'};	//这不是一个字符串，这只是一个字符数组
char cat[8] = {'f','a','t','e','s','s','a','\0'}	//这是一个字符串
```

将字符数组初始化为一个字符串的另一种方法：

```c++
char bird[11] = "Mr. Cheeps";	//'\0'被自动的存进最后一位
char fish[] = "Bubbles";		//编译器自动计算数组长度,并在末尾自动添加'\0'字符
```

应该确保数组足够大，能够存储所有的字符，包括末尾的空字符

在确定存储字符串所需的==最短数组==时，要将末尾的==空字符计算在内==

如果将字符串中的**某一位变为空字符**，那么这个**字符后的字符串**字符将都会变**为空字符**

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    char name[] = "Basicman";
    name[3] = '\0';
    //第四个位置变为空字符后，字符串输出时将只输出前三个字符Bas
    //第四个字符后的字符(包括第四个字符)将都变为空字符'\0'
    cout << name << endl;

    system("pause");
    return 0;
}
```

2.字符串常量(**双引号**)==不能==与字符常量(**单引号**)互换

3.strlen()函数的使用：只计算==可见==的字符，并不把空格字符计算在内，数组的长度不能小于strlen(字符串)+1

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    char name[] = "Basicman";
    cout << strlen(name) << endl;
    //此时输出结果为8，不包含末尾的空格字符
    system("pause");
    return 0;
}
```

4.++ch与ch+1的区别

```c++
//若再cout中使用++ch,则输出的仍然是字母
//若在cout中使用的是ch+1，由于常量1是int类型变量，因此其运算结果会转换为int类型。
```

### 4.2.1 cin>>

1.cin>>使用空白(**空格、制表符和换行符**)来确定字符串的**结束位置**，这意味着cin在获取字符数组输入时只读取一个单词

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    char teacher[20];
    char student[20];

    cout << "Enter teacher name : ";
    cin >> teacher;

    cout << "Enter student name : ";
    cin >> student;

    cout << "Teacher is : " << teacher << endl;
    cout << "Student is : " << student << endl;
    system("pause");
    return 0;
}
```

如果第一次输入的名字内带有空格，将会是如下的输出：

![6781ce10c190401883858ad8ee8f5da7](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/6781ce10c190401883858ad8ee8f5da7.png)



由于cin将空格视作结尾，所以teacher只读取到了空格前的Bod，而其他数据则被**保存在输入队列**中；在student输入的时候，将会自动输入进student数组，导致student数组保存为Jmas。

所以在使用cin进行输入时，要注意是否有空格等输入，如果有的话要换方法。

2.使用cin的输入，**换行符会被保留在输入队列**中，但如果两次输入都是使用的cin，那么cin会自动**跳过**这个**换行符**(也包括**空字符**)。

### 4.2.2 cin.getline()

getline()函数读取一行输入，直到到达换行符，随后getline()**丢弃换行符**，存储字符串时，使用**空字符来结尾**。

```c++
cin.getline(数组名,字符数);
//示例：
char arr[20];
cin.getline(arr,20);
```

第一个参数是用来存储输入行的**数组的名称**，第二个参数是要**读取的字符数**。如果这个参数为20，则函数**最多读取19个字符**，剩余空间**自动在末尾添加空字符**。getline()成员函数在读取**指定数目的字符**或**遇到换行符**时停止读取。

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    char teacher[20];
    char student[20];

    cout << "Enter teacher name : ";
    cin.getline(teacher, 20);

    cout << "Enter student name : ";
    cin.getline(student, 20);

    cout << "Teacher is : " << teacher << endl;
    cout << "Student is : " << student << endl;
    system("pause");
    return 0;
}
```



![36b942e3624216ee905f414103f22253](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/36b942e3624216ee905f414103f22253.png)



### 4.2.3 cin.get()

get()函数读取一行输入，直到到达换行符，随后get()将**换行符保留在输入序列中**

```c++
cin.get(数组名,字符数);
//示例：
char arr[20];
cin.get(arr,20);
```

第一个参数是用来存储输入行的**数组的名称**，第二个参数是要**读取的字符数**。但如果要连续两次调用get()函数，由于第一次调用后换行符保留在了输入队列中，第二次将不会读取到数据，为了避免这中情况，应该将**第一次读取的换行符再使用get()函数读取掉**

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    char teacher[20];
    char student[20];

    cout << "Enter teacher name : ";
    cin.get(teacher, 20);
    cin.get();	//读取输入队列中留下的换行符

    cout << "Enter student name : ";
    cin.get(student, 20).get();	//将输入队列中剩下的换行符稀释掉

    cout << "Teacher is : " << teacher << endl;
    cout << "Student is : " << student << endl;
    system("pause");
    return 0;
}
```

![36b942e3624216ee905f414103f22253](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/36b942e3624216ee905f414103f22253.png)

示例中的两种稀释换行符的操作都是可以的。

```c++
//第一次输入
cin.get(teacher, 20);
cin.get();	//读取输入队列中留下的换行符
//第二次输入
cin.get(student, 20).get();	//将输入队列中剩下的换行符稀释掉
```



|        |                            cin>>                             |           cin.getline()            |                          cin.get()                           |
| :----: | :----------------------------------------------------------: | :--------------------------------: | :----------------------------------------------------------: |
| 换行符 | 保留，但如果两次连续输入都是cin>>，那么这么换行符在第二次输入时会被自动跳过 | 丢弃换行符，并使用空字符来作为结尾 | 保留换行符，如果想连续两次使用cin.get()函数，需要清除上一次输入留下的换行符 |
|        |                                                              |                                    |                                                              |
|        |                                                              |                                    |                                                              |



### 4.2.4 混合输入字符串和数字

由于使用cin>>读取输入时，换行符会被保留在输入队列中，所以如果在使用getline()或get()函数时，如果不清除这个换行符，会造成输入不正确的后果

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    int year;
    cout << "Enter the year(int) : ";
    cin >> year;

    char teacher[20];
    cout << "Enter teacher name : ";
    cin.getline(teacher, 20);

    cout << "Year is : " << year << endl;
    cout << "Teacher is : " << teacher << endl;


    system("pause");
    return 0;
}
```

![c8a8fac2d2f158cea474a224539f8d58](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/c8a8fac2d2f158cea474a224539f8d58.png)

由于cin>>输入数字后，换行符被保留在了输入队列中，所以Teacher数组无法读取到数据

为了解决这个问题，需要在数组读取前加入一个get()函数，来达到清除换行符的效果

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
    int year;
    cout << "Enter the year(int) : ";
    cin >> year;
    cin.get();

    char teacher[20];
    cout << "Enter teacher name : ";
    cin.getline(teacher, 20);

    cout << "Year is : " << year << endl;
    cout << "Teacher is : " << teacher << endl;


    system("pause");
    return 0;
}
```

![579b143080f982018f795d7d26757c07](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/579b143080f982018f795d7d26757c07.png)





### 4.2.5 C风格字符串函数

strlen()只计算==可见==的字符，并不把空字符计算在内，数组的长度==不能短于strlen(字符串)+1==。

strcpy(charr1,charr2)	//字符串2复制到字符串1。

strcat(charr1,charr2)	//字符串2附加到字符串1末尾。

strcmp(charr1,charr2)	//两个字符串**相同返回0**，1再2之前返回负值，2再1之前，返回正值。

例子如下：

```c++
#include <iostream>
#include <cstring>
using namespace std;

const int SIZE = 20;

int main()
{
	char F_Name[SIZE], L_Name[SIZE];
	char FULL_Name[SIZE * 2];

	cout << "Enter your first name: ";
	cin.getline(F_Name, SIZE);

	cout << "Enter your last name: ";
	cin.getline(L_Name, SIZE);

	cout << "Here's the information in a single string: ";
	
    //不懂为什么要用_s，不用的话系统报错
	strcpy_s(FULL_Name, F_Name);	//复制
	strcat_s(FULL_Name, ", ");		//连接
	strcat_s(FULL_Name, L_Name);	//连接

	cout << FULL_Name << endl;

	system("pause");
	return 0;
}
```

![b8c26349a2ddc7afc8f4c4ad1abf2551](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/b8c26349a2ddc7afc8f4c4ad1abf2551.png)





## 4.3 string类简介

1.**可以使用数组表示法来访问存储在string对象中的字符**,不同于C风格字符串，string对象**不使用空字符**来标记字符串**结尾**

2.对于string类型字符串输入时想输入**一整句话而不是一个单词**的方法：

```c++
getline(cin,str);//其中的str是定义的string类型的数组名
```

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string name, dessert;
    
	cout << "Enter your name: " << endl;
	getline(cin, name);	//输入Dirk Hammernose时不会影响下一行的输入
    
	cout << "Enter your favorite dessert: " << endl;
	getline(cin, dessert);	//输入Radish Torte时不会影响下一行的输入
    
	cout << "I have some delicious " << dessert;
	cout << "for you, " << name << endl;

	system("pause");
	return 0;
}
```

![d24c147c494872cb2551f1f981f0e7d9](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/d24c147c494872cb2551f1f981f0e7d9.png)

3.可以使用size()函数得到string类型字符串中**可视字符的长度**

```c++
string str1 = "Bob";
cout << str1.size() << endl;	//此时将输出3
```

4.string类字符串可以**直接进行加减运算**：

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string F_Name, L_Name;

	cout << "Enter your first name: ";
	getline(cin, F_Name);
	cout << "Enter your last name : ";
	getline(cin, L_Name);

	F_Name = F_Name + ", " + L_Name;	//将首名和末名之间通过逗号和空格连接起来

	cout << "Here's the information in a single string: " << F_Name << endl;

	system("pause");
	return 0;
}
```

![53dc63dbbade9265272c4c47b7312376](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/53dc63dbbade9265272c4c47b7312376.png)





-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

==以下尚属未知形态==

3.string类型的数组模式是：

```c++
string Month[] = {"1","2","3","4","5","6","7","8","9","10","11","12"};
```

使用char*数组：

```c++
char *Month = { "1","2","3","4","5","6","7","8","9","10","11","12" };
```

4.字符总数中==包含回车键生成的换行符==。

----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## 4.7 指针和自由存储空间

1.指针是一个变量，存储的是值的地址，而不是值本身

```c++
int a = 10;
int *p = &a;
```

2.一定要在对指针**解除引用运算符(*)之前**，将指针初始化为一个**确定的、适当的地址**。

3.将指针变量加1后，其增加的值等于**指向的类型占用的字节数**

4.通常情况下，C++将**数组名**视为数组的**第一个元素的地址**。





# 第5章 循环和关系表达式

## 5.1 for循环

1.for表达式中的判断值将被判定为**bool值**true或false

2.a++表示先用a再++，++a表示**先++再用a**。

## 5.2 while循环

1.类型别名：

```c++
#define BYTE char		//BYTE成为char的别名
//通用格式：
typedef typename aliasName;
//示例：
typedef char byte;		//byte成为char的别名
typedef char* byte_pointer	//byte_pointer成为char*的别名
```

typedef不会创建新类型，而只是==为已有的类型建立一个新名称==。

## 5.5 循环和文本输入

==逐字的读取来自文件或键盘的文本==。

1.使用原始的cin进行输入：

```c++
#include <iostream>
using namespace std;

int main()
{
	char ch;		//定义输入的字符
	int count = 0;	//定义被读取的字符数值
	cout << "Enter characters; enter # to quit:" << endl;
	cin >> ch;		//输入字符
	//如果输入的字符不是'#'，那么循环继续，程序将继续读入字符进ch
	//虽然输入的时候是一整串字符串，但是读入的时候未读入的会保留在输入队列
	//当判断完成后，在while循环内继续读取输入队列中的字符串
	while (ch != '#')
	{
		cout << ch;
		count++;
		cin >> ch;
	}
	//每当有一个字符被读入进while循环内时，count将会+1
	//空字符由于cin的特性，并不会被读入while循环内
	cout << endl << count << " characters read" << endl;

	system("pause");
	return 0;
}
```

![fb3be711c88510f6af7810a68f50194a](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/fb3be711c88510f6af7810a68f50194a.png)

使用cin读取字符时，**空格字符并不会被读入**。更为复杂的是，只有用户**按下回车键**后，它输入的内容**才会发送给程序**。

-----------------------------------------------------------------

2.使用cin.get(char)进行补救

成员函数cin.get(char)读取输入中的下一个字符(**即使他是空格**)，并将其赋值给变量ch，使用这个函数替换cin>>ch，将会改善没读空格的问题

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
	char ch;		//定义输入的字符
	int count = 0;	//定义被读取的字符数值
	cout << "Enter characters; enter # to quit:" << endl;
	cin.get(ch);		//输入字符
	//如果输入的字符不是'#'，那么循环继续，程序将继续读入字符进ch
	//虽然输入的时候是一整串字符串，但是读入的时候未读入的会保留在输入队列
	//当判断完成后，在while循环内继续读取输入队列中的字符串
	while (ch != '#')
	{
		cout << ch;
		count++;
		cin.get(ch);
	}
	//每当有一个字符被读入进while循环内时，count将会+1
	cout << endl << count << " characters read" << endl;

	system("pause");
	return 0;
}
```

![f5bfed1392a491e2bdb9eee0fdecd09f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f5bfed1392a491e2bdb9eee0fdecd09f.png)





## 5.9 编程练习

8.编写一个程序，使用char数组和循环每次读取一个单词，直到读到done为止；输出有多少个单词(不包括done)。

```c++
#include <iostream>
#include <cstring>
using namespace std;

int main()
{
	char ch[20];	//定义读入的数组名
	int count = 0;	//定义单词个数
	cout << "Enter words (to stop, type the word done) :" << endl;
	cin >> ch;
	//当读入的单词不等于done时，数字相加，并再次读入新的单词
	//strcmp()函数，二者相同时返回0
    //cin函数读到空格时将会停止输入，并将后续文本保留在输入队列中
	while ( strcmp(ch,"done") )
	{
		count++;
		cin >> ch;
	}

	cout << "You entered a total of " << count << " words." << endl;

	system("pause");
	return 0;
}
```

![f2145e7e427112ab9cb33a45df66e30a](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/f2145e7e427112ab9cb33a45df66e30a.png)

9.编写一个程序，使用string和循环每次读取一个单词，直到读到done为止；输出有多少个单词(不包括done)。

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
	string ch;	//定义读入的数组名
	int count = 0;	//定义单词个数
	cout << "Enter words (to stop, type the word done) :" << endl;
	cin >> ch;
	//当读入的单词不等于done时，数字相加，并再次读入新的单词
	//string字符串可以直接使用算术运算符
    //cin函数读到空格时将会停止输入，并将后续文本保留在输入队列中
	while ( ch!="done" )
	{
		count++;
		cin >> ch;
	}

	cout << "You entered a total of " << count << " words." << endl;

	system("pause");
	return 0;
}
```

![a1d81e562ba2dea80fa7269e345c4b54](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/a1d81e562ba2dea80fa7269e345c4b54.png)



# 第6章 分支语句和逻辑运算符

## 6.1 if语句

1.if测试条件也将被强制转为bool值，因此0将被转换为false，非零为true。

2.记录用户输入'.'之前的所有字符数，并记录输入的空格数：

```c++
#include <iostream>
#include <string>
using namespace std;

int main()
{
	char ch;		//定义输入的字符
	int space = 0;	//定义空格的数量
	int total = 0;	//定义在'.'之前被读取的字符数值
	cin.get(ch);		//输入字符
	//读取'.'之前的所有字符
	while (ch != '.')
	{
		//记录空格的字符数
		if (ch == ' ')
		{
			space++;
		}
		total++;	//记录总的字符数,包括回车
		cin.get(ch);
	}
	cout << "一共有空格" << space << "个" << endl;
	cout << "一共有字符" << total << "个" << endl;

	system("pause");
	return 0;
}
```

![3f281c2f97afdd6fb9ef6dc22e855c31](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3f281c2f97afdd6fb9ef6dc22e855c31.png)

注意，字符总数中**包括**回车键生成的**换行符**。

## 6.2 逻辑表达式

1.||运算符先修改左侧的值，再对右侧的值进行判定。如果==左侧的表达式为true，则C++将不会去判断右侧的表达式==。

2.&&运算符如果==左侧为false，则右侧表达式将不会被判定与计算==。

3.优先级：and(&&)>or(||)>not(!)。

4.对于两次取反后!!x，数值是否不变的解释：

当x是布尔值时，两次取反并不影响。但当x是其他类型值时，两次取反并不是原数值，而是布尔值。

## 6.3 字符函数库cctype

| 函数名称   | 返回值                                                       |
| :--------- | :----------------------------------------------------------- |
| isalnum()  | 如果参数是字母数字，即字母或数字，该函数返回true             |
| isalpha()  | 如果参数是字母，返回true                                     |
| incntrl()  | 如果参数是控制字符，返回true                                 |
| isdigit()  | 如果参数是数字(0~9)，返回true                                |
| isgraph()  | 如果参数是除空格外的打印字符，返回true                       |
| islower()  | 如果参数是小写字母，返回true                                 |
| isprint()  | 如果参数是打印字符(包括空格)，返回true                       |
| ispunct()  | 如果参数是(标点符号)，返回true                               |
| isspace()  | 如果参数是标准空包字符，如空格、进纸、换行符、回车、水平制表符或垂直制表符，返回true |
| isupper()  | 如果参数是大写字母，返回true                                 |
| isxdigit() | 如果参数是十六进制数字，即0~9、a~f或A~F，返回true            |
| tolower()  | 如果参数是大写字符，返回其小写，否则返回该参数               |
| toupper()  | 如果参数是小写字符，返回其大写，否则返回该参数               |

## 6.5 switch语句

switch语句的通用格式：

```c++
switch(integer_expression)
{
    case labe11:statement(s)
    case labe12:statement(s)
        
    default:statement(s)    
}
```

1.integer_expression必须是一个结果为整数值的表达式，最常见的标签是int或char类型，也可以是枚举量

2.为应对不按指示办事的用户，**最好使用字符输入**



## 6.7 读取数字的循环

如果输入的变量类型与定义的变量类型不匹配，cin函数会发生以下四种情况

1.n的值保持不变

2.不匹配的输入将被留在输入队列中

3.cin对象中的一个错误标记被设置

4.对cin方法的调用将返回false(如果被转换为bool类型)。

也就是说，如果输入的值类型与定义的变量==不匹配==，那么cin>>函数将==返回false值==，并且将输入的数据==保留在队列==中



下面是一个让用户输入五个高尔夫得分的程序，如果输入的不是成绩则需要让用户重新输入：

```c++
#include <iostream>
using namespace std;
const int MAX = 5;


int main()
{
	int golf[MAX];	//定义高尔夫成绩数组
	cout << "Please Enter your golf scores." << endl;	//提示用户输入高尔夫成绩
	int i;
	for (int i = 0; i < MAX; i++)
	{
		cout << "rount #" << i + 1 << ": ";
		//如果用户输入的是数字，则不进入第一个while循环
		//如果用户输入的不是数字，则进入第一个while循环
		while (!(cin >> golf[i]))
		{
			//当用户输入的不是数字进入循环后，需要清除队列中的数据
			cin.clear();
			//在换行符以前的数据都被清理，当最后一个换行符被读入cin.get()函数内部后
			//程序将输出cout语句
			while (cin.get() != '\n')
			{
				continue;
			}
			cout << "Please enter a number:";
		}
	}
	system("pause");
	return 0;
}
```

![778698bebc0f5f7c6a887b674c4a26b6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/778698bebc0f5f7c6a887b674c4a26b6.png)

关键代码解释：

```c++
//当输入的不是数字时，cin>>会返回false，取反后才能进入循环
while (!(cin >> golf[i]))
	{
		//当用户输入的不是数字进入循环后，需要清除队列中的数据
		cin.clear();
		//在换行符以前的数据都被清理，当最后一个换行符被读入cin.get()函数内部后
		//程序将输出cout语句
		while (cin.get() != '\n')
		{
			continue;
		}
		cout << "Please enter a number:";
	}
```



# 第7章 函数——C++的编程语块

## 7.1 函数的基本知识

1.如果想使用C++函数，则必须完成：

- 提供函数定义


- 提供函数原型


- 调用函数

2.C++对于**返回值**的类型有一定的限制，**不能是数组**，但可以是其他任何类型

3.C++的编程风格是将**main()放在最前面**，因为它通常提供了程序的整体结构

4.原型的功能：通常，在原型的参数列表中，可以包括变量名，也可以不包括，原型中的变量名相当于占位符，因此不必与函数定义中的变量名相同，原型定义例子：

```c++
void func(int a,double b);
```

## 7.2 函数参数和按值传递



## 7.3 函数和数组

1.通常在函数中传递数组时，需要将数组名和数组长度传递进去

2.在函数定义中，使用

```c++
void func(int arr[],int len);
```

```c++
void func(int *arr,int len);
```

这两条语句是一样效果的

```c++
//在C++中，当且仅当用于函数头或原型函数中
int *arr 与 int arr[]的含义才是相同的
```

```c++
arr[i] == *(arr+i);
&arr[i] == arr+i
//这两个恒等式在函数中成立
```

3.对于函数中传递的数组名使用sizeof只会**得到数组名对应的指针长度**，不会得到数组长度，所以对数组的具体使用长度应该包含在函数当中。

4.由于函数接收的是数组的首地址，所以如果不想在函数中修改数组，应如下定义：

```c++
void func(const int *arr,int len);
void func(const int arr[],int len);
```

5.传统的确认数组区间的方法是直接传递给函数，但是也可以通过传递两个指针的方法来完成

一个指针标识数组的开头，一个指针标识数组的尾部，例子如下：

```c++
//通过首位指针确定数组长度
#include <iostream>
using namespace std;
const int SIZE = 8;
int func(const int* begin, const int* end);	//通过传递首地址和尾地址对数组数据相加的函数

int main()
{
	int arr[SIZE] = {1, 2, 4, 8, 16, 32, 64, 128};	//定义一个int数组，其中有8个数据
	//将数组所有元素全部传递给sum()函数
	//arr指向第一个元素，arr+SIZE指向数组结尾后面的一个位置
	int sum1 = func(arr, arr + SIZE);	
	cout << "sum1 = " << sum1 << endl;
	//令前四个数据相加：
	int sum2 = func(arr, arr + 4);
	cout << "sum2 = " << sum2 << endl;
	//令后四个数据相加：
	int sum3 = func(arr + 4, arr + SIZE);
	cout << "sum3 = " << sum3 << endl;

	system("pause");
	return 0;
}

int func(const int* begin, const int* end)
{
	int total = 0;	//完成数组相加总值的函数
	const int* p;	
	//令指针p指向要处理的第一个元素，通过循环来更新指针p
	//当指针p等于end，这时它指向最后一个元素后面的位置，循环结束
	for (p = begin; p < end; p++)
	{
		total = total + *p;
	}
	return total;
}
```

![4c6546374125b6d316d61b7679ea8c1b](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4c6546374125b6d316d61b7679ea8c1b.png)

可以通过传递首尾指针来确定范围，举个例子，如果函数想使用数字内的所有元素，那么传递时，可以传递首指针和最后一个元素后面一个位置的指针。

## 7.5 函数和C风格字符串

### 7.5.1 将C风格字符串作为参数的函数

1.将C风格字符串作为参数的函数，通常传递的时字符串指针，由于字符串有内置的结束字符，所以函数可以使用循环来依次检查字符串中的每个字符，直到遇到结尾的空值字符为止。

```c++
#include <iostream>
using namespace std;

//使用一个函数来计算m和u在字符串中出现的次数

unsigned int func(const char* ptr, char ch);

int main()
{
	//定义两个字符串
	char ch1[20] = "minimum";
	char ch2[20] = "uiulate";
	//通过函数func读取字符串1中m的个数和字符串2中u的个数
	//传递字符串指针给函数，并且指针指向的是字符串的首地址
	unsigned int num_m = func(ch1, 'm');
	unsigned int num_n = func(ch2, 'u');
	//使用cout输出字符串时，只需要把字符串的数组名放在其中即可
	cout << num_m << " m characters in " << ch1 << endl;
	cout << num_n << " u characters in " << ch2 << endl;

	system("pause");
	return 0;
}

unsigned int func(const char* ptr, char ch)
{
	//ptr指针指向字符串的第一个字符，因此*ptr表示的是第一个字符
	unsigned int num = 0;
	//由于字符串以空字符为结尾，所以当没读取到结尾时，程序一直进入循环
	while (*ptr)
	{
		if (*ptr == ch)
		{
			num++;
		}
		ptr++;
	}
	return num;
}
```

![aadd29be8f2418bfa63706e0571007a2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/aadd29be8f2418bfa63706e0571007a2.png)

2.定义字符串时，数组名就是字符串的指针，它指向字符串第一个元素的地址

3.处理字符串中字符的标准方法：

```c++
while(*ptr)
{
    statements;	//处理字符串字符的程序
    ptr++;
}
```

4.使用cout输出C风格的字符串时，只需将字符串名放进cout内即可：

```c++
char ch1[20] = "minimum";
cout << ch1;	//输出的即是minimum
```

### 7.5.2 返回C风格字符串的函数

1.函数无法返回一个字符串，但是可以返回字符串的地址

```c++
#include <iostream>
using namespace std;

//给函数输入一个字符ch和整数n
//函数返回一个包含n个相同字符ch的字符串
//例如func(a,4),那么函数返回一个aaaa的字符串
char* func(char ch, int n);

int main()
{
	//定义要用户输入的字符和数字
	char ch;
	int n;
	//提示用户输入字符和数字
	cout << "请输入一个字符:";
	cin >> ch;
	cout << "请输入一个数字:";
	cin >> n;
	//返回一个包含n个相同字符ch的字符串ptr
	//指针ptr指向这个字符串第一个字符的地址
	char* m_ptr = func(ch, n);
	//输出这个字符串
	cout << "通过函数func()得到的字符串为：" << m_ptr << endl;
	//由于返回的指针是使用new字符在堆区开辟的，所以需要使用delete释放
	delete[] m_ptr;
	system("pause");
	return 0;
}

char* func(char ch, int n)
{
	//使用关键字new在堆区创建一个长度与数字参数相同的字符串
    //这里必须是n+1而不能是n，因为要生成的字符就有n个
    //为了让最后一位字符是空字符，必须创建n+1个位置
	char* ptr = new char[n+1];
	//令字符串的最后一位是空字符
	ptr[n] = '\0';
	//将最后一位之前每个元素都初始化为该字符
	int i = 0;
	while (i < n)
	{
		ptr[i] = ch;
		i++;
	}
	//返回指向新字符串的指针
	return ptr;
}
```

![e1a4ebe4717f7392d91612a174299366](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e1a4ebe4717f7392d91612a174299366.png)

2.在函数中通过new创建的指针，在main函数中要使用delete稀释

3.在函数中创建的字符串数组，最好使用new来开辟，否则返回的指针可能报错

## 7.6 函数和结构

1.使用结构编程时，最直接的方式是像处理基本类型那样来处理结构，也就是说，将结构作为参数传递，并在需要时将结构用作返回值使用。

```c++
#include <iostream>
using namespace std;

//定义一个包含小时和分钟的结构
struct m_time
{
	int hours;
	int mins;
};

//函数1通过传递两个结构，计算两个结构的总体小时和分钟
m_time func1(m_time t1, m_time t2);
//函数2通过传递一个结构体，展示现有的小时与时间
void func2(m_time t);

int main()
{
	//定义两个结构体并分别赋值
	//结构第一位为小时h，第二位为分钟m
	m_time t1 = { 5,45 };
	m_time t2 = { 4,55 };
	m_time total = func1(t1, t2);
	//展示前两天总共的小时与分钟
	cout << "Two-day total: ";
	func2(total);

	m_time t3 = { 4,32 };	//定义第三天的小时与分钟
	//展示前三天总共的小时与分钟
	cout << "Three-day total: ";
	func2(func1(total, t3));

	system("pause");
	return 0;
}

m_time func1(m_time t1, m_time t2)
{
	m_time total;
	//计算总小时
	total.hours = t1.hours + t2.hours + (t1.mins + t2.mins)/60;
	//计算总分钟
	total.mins = (t1.mins + t2.mins) % 60;
	//返回结构体
	return total;
}

void func2(m_time t)
{
	cout << t.hours << " hours , " << t.mins << " minutes" << endl;
}
```

![799e5412cceff9b605b1988d603fe6fb](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/799e5412cceff9b605b1988d603fe6fb.png)

2.对结构体的使用可像普通变量一样