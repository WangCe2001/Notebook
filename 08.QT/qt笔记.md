# 一.创建Qt项目及概述

## 1.创建教程

1.选择第一个创建QT桌面

![image-20241101222800675](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101222800675.png)

2.创建文件名称和存储路径

- 名称里面==不能用中文和空格==
- 创建路径==不能有中文==
- 无需设为默认路径

![image-20241101223131601](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101223131601.png)

3.可以选择使用qmake语法做为编译基础

![image-20241101223255952](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101223255952.png)

4.创建类信息：

![image-20241101223621394](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101223621394.png)

此时创建类时可以有三种类型：

![image-20250217172821991](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250217172821991.png)



![image-20241101224743350](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101224743350.png)

父类QWidget是创建一个空窗口

子类QMainWindow会增加一行菜单栏、工具、状态栏等

子类QDialog是创建对话框





5.选择上面的这个做为编译环境，下面那个用的是VScode

![image-20241101223820638](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241101223820638.png)

6.其他的选择下一步即可，创建成功后如下所示：

![image-20250220085026641](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250220085026641.png)

7.代码解释：

```c++
#include "mywidget.h"
#include <QApplication> //包含一个应用程序类的头文件

//main程序入口  argc命令行变量的数量  argv命令行变量的数组
int main(int argc, char *argv[])
{
    //a应用程序对象，在Qt中，应用程序对象，有且仅有一个
    QApplication a(argc, argv);
    //窗口对象 mywidget父类 -> Qwidget
    mywidget w;
    //窗口对象 默认不会显示，必须要调用show方法显示窗口
    w.show();
    //让应用程序对象进入消息循环，将代码堵塞到这行
    return a.exec();
}
```



## 2.FirstProject.pro文件注释

pro文件的注释即解释：

```makefile
QT       += core gui	#QT包含的模块

greaterThan(QT_MAJOR_VERSION, 4): QT += widgets		#大于4版本以上 包含widget模块

CONFIG += c++17

# You can make your code fail to compile if it uses deprecated APIs.
# In order to do so, uncomment the following line.
#DEFINES += QT_DISABLE_DEPRECATED_BEFORE=0x060000    # disables all the APIs deprecated before Qt 6.0.0

SOURCES += \			#源文件
    main.cpp \
    mywidget.cpp

HEADERS += \			#头文件
    mywidget.h

TRANSLATIONS += \
    01_FirstProject_zh_CN.ts
CONFIG += lrelease
CONFIG += embed_translations

# Default rules for deployment.
qnx: target.path = /tmp/$${TARGET}/bin
else: unix:!android: target.path = /opt/$${TARGET}/bin
!isEmpty(target.path): INSTALLS += target
```



第一行QT包含的模块：

![Qt5 模块](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/Qt5%20%E6%A8%A1%E5%9D%97.png)

第二行语句的意思：在早期的QT版本中，Widgets模块是包含在GUI模块内的，但是在QT5版本后，Widgets被单独分裂出一个模块，为了兼容早期的代码，可以使用第二行语句，使得如果这个QT模块是在版本4以上的，则包含Widgets模块



注意：尽量不要在pro文件中写注释等其他文字，否则会报错



## 3.mywidget .h文件注释

源文件：

```c++
#ifndef MYWIDGET_H
#define MYWIDGET_H

#include <QWidget>

class mywidget : public QWidget
{
    Q_OBJECT

public:
    mywidget(QWidget *parent = nullptr);
    ~mywidget();
};
#endif // MYWIDGET_H
```

解释文件：

```c++
#ifndef MYWIDGET_H
#define MYWIDGET_H
/*
这两行代码是头文件保护符（Include Guard）。它的作用是防止头文件被重复包含，导致编译错误。在编译过程中，如果 MYWIDGET_H 没有被定义，则会定义它并继续处理头文件的内容。如果它已经被定义（说明头文件已经被包含过），则编译器会跳过这段代码。
*/

#include <QWidget>	//包含头文件 Qwidget窗口类

/*
这里引入了 QWidget 类，这是 Qt 中的一个基础类，表示一个窗口部件（Widget）。QWidget 是所有用户界面对象的基类，其他窗口部件（如按钮、标签等）都继承自它。
*/

class mywidget : public QWidget
{
    Q_OBJECT	//Q_OBJECT宏，允许类中使用信号和槽的机制
/*
1.class mywidget : public QWidget
	定义了一个名为 mywidget 的类，并且它继承自 QWidget。
	这表明 mywidget 是一个自定义的窗口部件，可以使用 QWidget 的所有功能，并能够扩展它。
2.Q_OBJECT
	这是一个宏，必须添加在继承自 QObject 或其子类（如 QWidget）的类中。
	它使得类能够使用 Qt 的信号与槽（Signals and Slots）机制，以及其他元对象特性（如动态属性、Qt 的事件系统等）。
	如果没有这个宏，信号与槽机制将无法正常工作。
*/
        
public:
    mywidget(QWidget *parent = nullptr);	//构造函数
    ~mywidget();							//析构函数
/*
1.mywidget(QWidget *parent = nullptr)
	这是 mywidget 类的构造函数。
	参数 QWidget *parent = nullptr 表示可以为这个窗口部件指定一个父窗口部件。如果没有指定父窗口部件（即参数为 nullptr），它将是一个顶层窗口。
	在 Qt 中，窗口部件通常是层级结构的，子窗口部件会跟随父窗口部件的生命周期。
2.~mywidget()
	这是 mywidget 类的析构函数。
	当 mywidget 对象被销毁时，析构函数会被调用，用于释放资源。
*/
};
#endif // MYWIDGET_H
//这对应头文件保护符的结束部分，与开头的 #ifndef 和 #define 配合使用，标志头文件的结束。
```



## 4.mywidget.cpp解释：

源文件：

```c++
#include "mywidget.h"

mywidget::mywidget(QWidget *parent)
    : QWidget(parent)
{}

mywidget::~mywidget() {}
```

解释文件：

```c++
#include "mywidget.h"
/*
这里通过 #include "mywidget.h" 将头文件 mywidget.h 中的声明引入到当前实现文件中。
头文件中定义了 mywidget 类及其接口，而 .cpp 文件中实现了这些接口的具体逻辑。
*/

mywidget::mywidget(QWidget *parent)
    : QWidget(parent)
{}
/*
1.mywidget::mywidget(QWidget *parent)
	这是 mywidget 类的构造函数。
	它实现了头文件中声明的构造函数。
	参数 QWidget *parent 允许为这个窗口部件设置一个父窗口部件。
		如果 parent 不为空，mywidget 将作为子窗口部件嵌套在父窗口部件中。
		如果 parent 为 nullptr（默认值），mywidget 将是一个顶层窗口。
2.: QWidget(parent)
	这是初始化列表，用于调用基类 QWidget 的构造函数，并将 parent 参数传递给它。
	这样可以正确设置父窗口部件，继承父类的相关特性（如位置、大小、生命周期等）。
3.**空函数体 {}
	当前构造函数的函数体为空，意味着没有额外的初始化逻辑。
	如果你需要在窗口创建时添加自定义逻辑（如设置窗口标题、大小、布局等），可以在这里实现。
*/
mywidget::~mywidget() {}
/*
1.mywidget::~mywidget()
	这是 mywidget 类的析构函数。
	它实现了头文件中声明的析构函数。
	当前析构函数的函数体为空 {}，意味着没有额外的资源释放逻辑。
	如果你的类中有动态分配的资源（如 new 创建的对象，或打开的文件），需要在这里释放，以防止内存泄漏。
2.父类析构
	即使函数体为空，当 mywidget 被销毁时，Qt 的对象树机制会自动销毁它的所有子对象，并调用基类 QWidget 的析构函数，确保资源被清理。
*/
```



## 5.main.cpp文件解释：

源文件：

```c++
#include "mywidget.h"
#include <QApplication>

int main(int argc, char *argv[])
{
    QApplication a(argc, argv);
    mywidget w;
    return a.exec();
    w.show();
}
```

解释文件：

```c++
#include "mywidget.h"
#include <QApplication>
/*
作用：包含头文件
1.#include "mywidget.h"
	包含自定义窗口部件 mywidget 的头文件，定义了 mywidget 类。
2.#include <QApplication>
	包含 Qt 的 QApplication 类，这是 Qt 应用程序的核心类，负责应用程序的初始化、事件循环等。
*/


int main(int argc, char *argv[])
{
    /*
    作用：主函数入口
    1.int main(int argc, char *argv[]) 是 C++ 程序的入口函数。
	2.参数说明：
		argc 是命令行参数的个数。
		argv 是一个指针数组，存储了命令行参数的值。
	3.在 Qt 应用程序中，这些参数会传递给 QApplication，以便处理应用程序的初始化参数
    */
    QApplication a(argc, argv);
    /*
    作用：创建应用程序对象
    1.QApplication
		QApplication 对象必须在任何 GUI 应用程序中创建，它负责管理应用程序的生命周期、事件循环和资源。
		它接收命令行参数 argc 和 argv，用于初始化应用程序。
		a 是 QApplication 类型的对象，后续调用 a.exec() 开启主事件循环。
    */
    mywidget w;
    /*
    作用：创建窗口对象
    定义了一个 mywidget 类型的对象 w。
	由于 mywidget 继承自 QWidget，它是一个窗口部件（Widget）。
	注意：虽然创建了这个窗口对象，但它默认是隐藏的，必须调用 w.show() 才会显示窗口。
    */
    
    w.show();
    
    return a.exec();
    /*
    作用：进入事件循环
	1.a.exec()
		启动 Qt 的事件循环，应用程序开始运行。
		它会不断检测用户输入（如鼠标点击、键盘输入）和系统事件，并分发给对应的窗口部件进行处理。
		事件循环会一直运行，直到调用 QApplication::quit() 或关闭所有顶层窗口时退出。
	2.return
		a.exec() 返回一个整数值，通常表示应用程序的退出状态。
    */
}
```





## 6.命名规范快捷键：

**1.命名规范：**

```
类名 首字母大写、单词和单词之间首字母大写
函数名 变量名称 首字母小写、单词和单词之间首字母大写
```

**2.快捷键：**

```
注释	ctrl+/
运行	ctrl+r
编译	crtl+b
字体缩放	ctrl+鼠标滚轮
查找	ctrl+f
整行移动	ctrl+shift+↑或↓
自动对齐	crtl+i
同名之间的.h 和 .cpp 切换	F4
帮助文档：
	第一中：F1
	第二种：左侧帮助按钮
	第三种：查看bin文件中的帮助手册
```

## 7.帮助文档

路径：D:\QT\6.5.3\mingw_64\bin\assistant.exe

打开后如图所示：

![image-20250219165541082](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250219165541082.png)

# 二.第一个Qt小程序



## 1.按钮的创建

通过查阅帮助文档可知，传承关系如下所示：

QPushButton->QAbstractButton->QWidget->QObject and QPaintDevice



```c++
#include "mywidget.h"
#include <QPushButton>  //按钮控件的头文件

mywidget::mywidget(QWidget *parent)
    : QWidget(parent)
{
    //创建一个按钮
    QPushButton *btn = new QPushButton;
    //btn->show();    //show以顶层方式弹出窗口控件
    //为了让btn对象依赖在myWidget窗口中
    btn->setParent(this);
    //显示文本
    btn->setText("第一个按钮");

    //创建第二个按钮 按照控件的大小创建窗口
    QPushButton *btn2 = new QPushButton("第二个按钮",this);
    //移动btn2按钮
    btn2->move(100,100);
    //按钮也可以重新制定大小
    btn2->resize(100,100);
    //重置窗口大小,传入宽和高
    resize(600,400);
    //设置固定窗口大小
    setFixedSize(600,400);
    //设置窗口标题
    setWindowTitle("第一个窗口");
}
mywidget::~mywidget() {}
```

输出结果：

![image-20250219182504390](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250219182504390.png)

## 2.对象树

在C++的继承语法中，

构造函数顺序：先调用**父类**构造函数，再调用==子类==构造函数

析构函数顺序：先调用==子类==构造函数，再调用**父类**构造函数

在Qt中：

当创建QObject对象时，可以提供一个其父对象，我们创建的这个QObject对象会自动添加到其父对象的children()列表

当父类对象析构的时候，这个列表中的所有对象也会被析构，注意，这里的父对象并不是继承意义上的父类

![Qt对象树](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/Qt%E5%AF%B9%E8%B1%A1%E6%A0%91.png)



做个实验：

1.在Qt项目中添加新文件：

![image-20250220141203727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250220141203727.png)

2.选择添加文件的类型：

![image-20250220141245795](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250220141245795.png)

3.如图所示创建自己的按钮：

![image-20250220141610990](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250220141610990.png)

生成的自己的按钮类头文件：

```c++
#ifndef MYPUSHBUTTON_H
#define MYPUSHBUTTON_H
#include <QPushButton>

class MyPushButton : public QPushButton
{
    Q_OBJECT
public:
    explicit MyPushButton(QWidget *parent = nullptr);
    ~MyPushButton();
signals:
};

#endif // MYPUSHBUTTON_H
```

生成的自己的按钮类.cpp文件：

```c++
#include "mypushbutton.h"
#include <QDebug>
MyPushButton::MyPushButton(QWidget *parent)
    : QPushButton{parent}
{
    qDebug()<< "我的按钮类构造调用";

}
MyPushButton::~MyPushButton()
{
    qDebug()<< "我的按钮类析构";

}
```

创建自己的按钮对象：

```c++
MyPushButton * myBtn = new MyPushButton;
myBtn->setParent(this);
myBtn->setText("我自己的按钮");
myBtn->move(200,0);
```

具体实现可查看01_FirstProject工程文件

当创建的对象在堆区时候，如果指定的父亲是QObject派生下来的类或者QObject子类派生下来的类，可以不用管理释放的操作，对象会被放入对象树中，在一定程度上简化了内存回收机制



## 3.Qt窗口坐标系

在Qt的坐标系中：(0,0)在左上角

X以右为正方向

Y以下为正方向

![Qt窗口坐标系](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/clip_image001.png)

# 三.信号和槽机制

所谓信号槽，实际就是观察者模式，当某个事件发生之后，它就会发出一个信号，如果有对象对这个信号感兴趣，它就会使用连接(connect)函数，将想要处理的信号和自己的一个函数(称为槽(slot)绑定来处理这个信号)，也就是说，当信号发出时，被链接的槽函数会自动被回调

![Qt信号和槽 ](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/Qt%E4%BF%A1%E5%8F%B7%E5%92%8C%E6%A7%BD%20.png)

## 1.系统自带的信号和槽



![image-20250220173209737](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250220173209737.png)





发送的信号可借助查照文档的signal来寻找

信号和槽之间通过connet()函数进行连接，参数定义如下：

参数1：信号的发送者    参数2：发送的信号(函数的地址)   参数3：信号的接收者  参数4：处理的槽函数(函数的地址)

```c++
//连接信号
connect(btn,&QPushButton::clicked,zt,teacherSignal2);
//断开信号
disconnect(zt, teacherSignal2, st, studentSlot2);
```

实现点击按钮窗口退出代码：

```c++
//需求：点击我的按钮，关闭窗口
//参数1：信号的发送者    参数2：发送的信号   参数3：信号的接收者  参数4：处理的槽函数
connect(myBtn, &MyPushButton::clicked, this, &myWidget::close);
connect(myBtn, &QPushButton::clicked, this, &QWidget::close);
```



## 2.自定义信号和槽

1.创建一个新项目，创建过程看标题一，创建成功后如图所示：

![image-20250221090941060](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250221090941060.png)

2.这个项目的需求如下：

```c++
//Teacher类  老师类
//Student类  学生类
//下课后，老师会触发一个信号，饿了  学生响应信号，请客吃
```



3.分别创建老师类和学生类，在并widget中调用，具体代码实现可看项目02_SingalAndSlot

- 具体规则：
  - 自定义信号：
    - 写到signals下
    - 返回void
    - 需要声明，不需要实现
    - 可以有参数，可以重载
  - 自定义槽函数
    - 返回void
    - 需要声明，也需要实现

老师类头文件：

```c++
#ifndef TEACHER_H
#define TEACHER_H

#include <QObject>

class Teacher : public QObject
{
    Q_OBJECT
public:
    explicit Teacher(QObject *parent = nullptr);
signals:
    //自定义信号 写到signals下
    //返回值是void，只需要声明，不需要实现
    //可以有参数，可以重载
    void hungry();
    void hungry(QString foodName);
};
#endif // TEACHER_H
```

老师类.cpp文件实现：

```c++
#include "teacher.h"

Teacher::Teacher(QObject *parent)
    : QObject{parent}
{}
```



学生类.h文件：

```c++
#ifndef STUDENT_H
#define STUDENT_H

#include <QObject>

class Student : public QObject
{
    Q_OBJECT
public:
    explicit Student(QObject *parent = nullptr);
    //早期Qt版本必须写在public sltos下，高级版本可以写到public或者全局作用域下
    //返回值void，需要声明，也需要实现
    //可以有参数，可以发生重载
    void treat();
    void treat(QString foodName);
signals:
};

#endif // STUDENT_H
```

学生类.cpp文件：

```c++
#include "student.h"
#include <QDebug>
Student::Student(QObject *parent)
    : QObject{parent}
{

}

void Student::treat()
{
    qDebug() << "请老师吃饭";
}

void Student::treat(QString foodName)
{
    //QString -> char* 先转成QByteArray (.toUtf8()) 再转成char* (.data())
    qDebug() << "请老师吃饭，老师要吃:" << foodName.toUtf8().data();
}
```



窗口文件建立二者联系：

```c++
//创建一个老师对象
this->zt = new Teacher(this);
//创建一个学生对象
this->st = new Student(this);
//10.自定义信号和槽
//连接不带参数的信号和槽
//老师饿了，学生请客连接
void(Teacher:: *teacherSignal1)() = &Teacher::hungry;
void(Student:: *studentSlot1)() = &Student::treat;
connect(zt, teacherSignal1, st, studentSlot1);
//调用下课函数，发送不带参数的信号，并用不带参数的槽接受，输出的是"请老师吃饭"
classIsOver();
```



## 3.当自定义信号和槽出现重载



- 需要利用函数指针明确指向函数的地址
- void(Teacher:: *teacherSignal)(QString) = &Teacher::hungry;
- QString 转成 char*
  - .toUtf8() 先转成QByteArray
  - .data() 再转为 char*

由于connect函数接收的是函数的地址，所以需要使用函数指针明确指明是哪个函数重载的地址

代码示例;

```c++
//11.自定义的信号和槽发生重载的解决
    //连接带参数的 信号和槽
    //指针 可以指向-> 地址
    //函数指针 -> 函数地址
    void(Teacher:: *teacherSignal)(QString) = &Teacher::hungry;
    void(Student:: *studentSlot)(QString) = &Student::treat;
    //将带参数的信号和槽建立联系
    connect(zt, teacherSignal, st, studentSlot);
    //调用下课函数，发送带参数的信号，并调用带参数的槽函数接受，输出的是"请老师吃饭，老师要吃，宫保鸡丁"
    classIsOver();


    //点击一个 下课的按钮，再触发下课
    QPushButton *btn = new QPushButton("下课",this);
    //重置窗口的大小
    this->resize(600,400);
    //点击按钮，触发classIsOver函数
    connect(btn,&QPushButton::clicked,this,&Widget::classIsOver);
    //点击按钮触发老师无参信号
    connect(btn,&QPushButton::clicked,zt,teacherSignal2);
    //断开信号，断开老师的无参信号与学生的无参槽函数连接
    disconnect(zt, teacherSignal2, st, studentSlot2);
    //断开后，点击按钮并不会触发无参槽函数的调用
```



## 4.信号连接信号

在Qt语法中，信号可以连接信号

```c++
//12.信号连接信号
    //拓展
    //1.信号是可以连接信号的
    //2.一个信号可以连接多个槽函数
    //3.多个信号 可以连接 同一个槽函数
    //4.信号和槽函数的参数 必须类型一一对应
    //5.信号和槽的参数个数 是不是要一致？信号的参数个数 可以多余槽函数的参数个数
```





## 5.Qt版本信号槽连接

```c++
//Qt4版本一起的信号和槽连接方式
//利用Qt4信号槽 连接无参版本 这种模式可能报错，因为定义的SLOT函数要在public slots下
//Qt4版本 底层SINGAL("hungry") SLOT("treat")
connect(zt, SIGNAL(hungry()), st, SLOT(treat()));
//Qt4版本优点，参数直观，缺点：类型不做检查 不推荐这种语法
//Qt5以上 支持Qt4的版本写法，反之不支持
```



## 6.lambda表达式

```c++
//14.lambda表达式
    QPushButton * btn2= new QPushButton;
    [btn](){
        btn->setText("aaaa");
        btn2->sexText("bbb");  //btn2看不到
    }();

    QPushButton * myBtn = new QPushButton (this);
    QPushButton * myBtn2 = new QPushButton (this);
    myBtn2->move(100,100);
    int m = 10;
    //加上mutable关键字后，每次点击都会输出110这个值，但是并不会改变m的本体
    //如果删除mutable关键字后，则值传递无法修改m的值
    connect(myBtn,&QPushButton::clicked,this,[m] ()mutable { m = 100 + 10; qDebug() << m; });
    connect(myBtn2,&QPushButton::clicked,this,[=] ()  { qDebug() << m; });
    qDebug() << m;

    //指明输出类型，此时将输出1000
    int ret = []()->int{return 1000;}();
    qDebug() << "ret = "<< ret ;

    //利用lambda表达式，实现点击按钮 关闭窗口操作以及输出槽函数
    QPushButton * btn2 = new QPushButton;
    btn2->move(100,0);
    btn2->setText("关闭");
    btn2->setParent(this);
    connect(btn2 ,&QPushButton::clicked ,this ,[=](){
        this->close();
        emit zt->hungry("宫保鸡丁");
    });
```

lambda表达式最常用：

```c++
[=](){};
```





# 四.QMainWindow

QMainWindow为用户提供主窗口程序类，包含一个菜单栏(Menu Bar)、多个工具栏(Tool bars)、多个锚接部件(Dock Widget)、一个状态栏(Status Bar)及一个中心部件(Central Widget)

## 1.菜单栏和工具栏

程序如下：

```c++
#include "mainwindow.h"
#include <QMenuBar>
#include <QToolBar>
#include <QDebug>
#include <QPushButton>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
{
    //重置窗口大小
    resize(600,400);

    //菜单栏 只能最多有一个
    //菜单栏创建
    QMenuBar *bar = menuBar();
    //将菜单栏放入窗口中
    setMenuBar(bar);
    //创建菜单
    QMenu *fileMenu = bar->addMenu("文件");
    QMenu *editMenu = bar->addMenu("编辑");

    //创建菜单项
    QAction * newAction = fileMenu->addAction("新建");
    //添加分隔符
    fileMenu->addSeparator();
    QAction * openAction = fileMenu->addAction("打开");


    //工具栏 可以有多个
    QToolBar * toolBar = new QToolBar(this);
    //将工具栏默认停留在左侧
    addToolBar(Qt::LeftToolBarArea,toolBar);

    //后期设置 只允许 左右停靠
    toolBar->setAllowedAreas(Qt::LeftToolBarArea | Qt::RightToolBarArea);
    //此时只能停留在左右侧，如果不是左右侧且松手，则此时会有一个浮动的块停留在页面
    //设置浮动
    toolBar->setFloatable(false);
    //设置移动(总开关)
    toolBar->setMovable(false);
    //工具栏中可以设置内容
    toolBar->addAction(newAction);
    //添加分割线
    toolBar->addSeparator();
    toolBar->addAction(openAction);
    //工具栏中添加控件
    QPushButton *btn = new QPushButton("aa",this);
    toolBar->addWidget(btn);

}

MainWindow::~MainWindow() {}
```

输出结果：

![image-20250225175142727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250225175142727.png)

## 2.状态栏、铆接部件、核心部件

```c++
//03.QMainWindow_状态栏、核心部件
    //状态栏 最多只有一个
    QStatusBar * stBar = statusBar();
    //设置到窗口中
    setStatusBar(stBar);
    //放标签控件
    QLabel * label = new QLabel("提示信息",this);
    stBar->addWidget(label);

    QLabel * label2 = new QLabel("右侧提示信息",this);
    stBar->addPermanentWidget(label2);

    //铆接部件(浮动窗口) 可以有多个
    QDockWidget * dockWidget = new QDockWidget("浮动",this);
    addDockWidget(Qt::BottomDockWidgetArea,dockWidget);
    //设置后期停靠区域，只允许上下
    dockWidget->setAllowedAreas(Qt::TopDockWidgetArea | Qt::BottomDockWidgetArea);

    //设置中心部件 只能有一个
    QTextEdit * edit = new QTextEdit(this);
    setCentralWidget(edit);
```

输出结果：

![image-20250226101739107](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226101739107.png)



## 3.资源文件添加

1.直接在UI界面中添加，注意这里的"新建"和"打开"只能使用英文创建，然后在右下侧改变名称

![image-20250227132541075](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227132541075.png)

2.在text一栏改变名字

![image-20250227132743615](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227132743615.png)

对于UI界面的资源文件添加过程：

1.复制准备添加的文件：

![image-20250226111321954](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226111321954.png)

2.将准备复制的文件添加到项目中，选择在Explorer中显示：

![image-20250226111500366](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226111500366.png)

3.将文件复制到文件夹中

![image-20250226111654631](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226111654631.png)

4.在项目中选择添加新文件

![image-20250226111912377](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226111912377.png)

5.添加Qt Resource File文件

![image-20250226114933342](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226114933342.png)

6.添加时创建文件名，这里起名为res，点击下一步完成默认创建

![image-20250226115019292](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226115019292.png)

7.创建成功后，如果想打开这个资源文件，需要选择Open in Editor

![image-20250226120610620](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226120610620.png)

8.打开后点击添加前缀，在Prefix行写下前缀名，这里起名为/

![image-20250226120724563](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226120724563.png)

9.点击添加文件，打开之前添加的image文件夹中的图片文件

![image-20250226120833945](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226120833945.png)

10.添加成功后，点击编译，编译后如图所示

![image-20250226120940358](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226120940358.png)

11.在主文件中使用ui语句添加文件

![image-20250226121125458](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226121125458.png)

12.此时的新建图标变为自己想要的这个样子

![image-20250226121209539](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250226121209539.png)

# 五.对话框QDialog

## 1.模态和非模态对话框创建

在UI界面中添加new控件，并用中文命名为新建

模态对话框与非模态对话框创建代码：

```c++
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QDialog>
#include <QDebug>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

    //点击新建按钮 弹出一个对话框
    connect(ui->actionnew ,&QAction::triggered,[=](){
        //对话框分类
        //模态对话框（不可以对其他窗口进行操作）  非模态对话框（可以对其他的窗口进行操作）
        //模态创建  阻塞
        QDialog dlg(this);
        dlg.resize(200,100);
        dlg.exec();
        qDebug() << "模态对话框弹出了" ;

        //非模态对话框
        QDialog * dlg2 = new QDialog(this);
        dlg2->resize(200,100);
        dlg2->show();
        //为了防止内存泄露，需要在关闭新窗口后，释放堆区数据
        dlg2->setAttribute(Qt::WA_DeleteOnClose);   //55号属性
        qDebug() << "非模态对话框弹出了" ;
    });

}

MainWindow::~MainWindow()
{
    delete ui;
}
```

创建的actionnew指针如下：

![image-20250227135707633](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227135707633.png)



## 2.消息对话框

使用对话框时，要导入头文件QMessageBox，具体使用方法可参考Qt帮助文档

```c++
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QDialog>
#include <QDebug>
#include <QMessageBox>
MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

    //点击新建按钮 弹出一个对话框
    connect(ui->actionnew ,&QAction::triggered,[=](){
        //06.消息对话框
        //错误对话框
        QMessageBox::critical(this,"critical","错误");
        //信息对话框
        QMessageBox::information(this,"info","信息");
        //参数1 父亲  参数2  标题  参数3  提示内容  参数4  按键类型  参数5  默认关联回车按键
        //提问对话框,默认是yes和no，这里改为Save和Cancel,第五个参数是修改回车默认选项的，此时回车默认选项为Cancel
        if(QMessageBox::Save == QMessageBox::question(this,"question","提问",QMessageBox::Save|QMessageBox::Cancel,QMessageBox::Cancel))
        {
            qDebug() << "选择的是保存";
        }
        else
        {
            qDebug() << "选择的是取消";
        }

        //警告对话框
        QMessageBox::warning(this,"warning","警告");
    });
}
MainWindow::~MainWindow()
{
    delete ui;
}
```

输出结果：

![image-20250227152006391](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227152006391.png)

## 3.其他标准对话框

```c++
#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QDialog>
#include <QDebug>
#include <QMessageBox>
#include <QColorDialog>
#include <QFileDialog>
#include <QFontDialog>
MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);

    //点击新建按钮 弹出一个对话框
    connect(ui->actionnew ,&QAction::triggered,[=](){
        //07.其他标准对话框
        //颜色对话框
        QColor color = QColorDialog::getColor(QColor(255,0,0));
        qDebug() << "r = " << color.red() << " g = " << color.green() << " b = " << color.blue();
        //文件对话框
        //参数1  父亲  参数2  标题  参数3  默认打开路径  参数4  过滤文件格式
        QString str = QFileDialog::getOpenFileName(this,"打开文件","D:\\01.MyStudy\\08.QT\\02.黑马程序员\\day2资料\\Doc", "(*.txt)");
        //选择打开文件夹下的txt文件，返回的是选取文件的文件路径
        qDebug() <<str;
        //字体对话框
        bool flag;
        QFont font = QFontDialog::getFont(&flag,QFont("华文彩云",36));
        qDebug() << "字体：" << font.family().toUtf8().data() << "字号:" << font.pointSize() << "是否加粗:" << font.bold() << "是否倾斜:" << font.italic();
    });
}

MainWindow::~MainWindow()
{
    delete ui;
}

```

输出结果：

![image-20250227151919896](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227151919896.png)



# 六.布局和常用控件

## 1.登录窗口布局

用户名选用:Label控件

密码选用：Line Edit

按钮选择：Push Button

对齐窗口：Widget

弹簧选择：Horizontal Spacer

想要修改窗口名字、限定窗口大小，都要在MainWindow中的属性修改即可

![image-20250227172643223](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227172643223.png)

输出结果：

![image-20250227172702438](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227172702438.png)



## 2.控件——按钮组

如果想使用图片，则需要先通过资源文件添加，然后才可以

1.对Push Button添加图片，属性中的iconSize选择资源，成功加载后即显示图片

![image-20250227173515917](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227173515917.png)

2.添加Tool Button按键：可以在右下角的属性界面选择UI设计

![image-20250227175223244](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227175223244.png)

3.添加选择按钮：Radio Button，但此时运行程序只能点击一个按钮，如果想分组点击，需要选择Group Box，将选择按钮放在一个组里

![image-20250227175924566](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227175924566.png)

如果想要实现男按钮默认被选择，而且点击女按钮会有消息发出，可写如下代码：

![image-20250227180544012](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250227180544012.png)

4.如果想实现多选按钮，需要使用Check Box控件



## 3.QListWidget控件

上面的控件需要基于数据库才能使用，下面的基于项目即可使用，这里选择下面层

![image-20250228090303186](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228090303186.png)

添加List View，添加后并写入诗，效果如下：

![image-20250228091205013](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228091205013.png)

为了让显示水平居中，如下所示：

```c++
//利用ListWidget写诗
    QListWidgetItem * item = new QListWidgetItem("锄禾日当午");
    //将一行诗放入到ListWidget控件中
    ui->listWidget->addItem(item);
    //让显示水平居中
    item->setTextAlignment(Qt::AlignHCenter);


    //QStringList  QList<QString>
    QStringList list;
    list << "锄禾日当午" << "汗滴禾下土" << "谁知盘中餐" << "粒粒皆辛苦";
    ui->listWidget->addItems(list);
```

![image-20250228162730238](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228162730238.png)



## 4.QTreeWidget树控件

选择控件中的Tree Widget控件，选择垂直居中，可以自动填满界面

![image-20250228174345230](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228174345230.png)

代码如下：

```c++
#include "widget.h"
#include "ui_widget.h"
#include <QString>

Widget::Widget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::Widget)
{
    ui->setupUi(this);

    //treeWidget树控件使用

    //设置水平头
    ui->treeWidget->setHeaderLabels(QStringList()<<"英雄"<<"英雄介绍");

    QTreeWidgetItem * liItem = new QTreeWidgetItem(QStringList()<<"力量");
    QTreeWidgetItem * minItem = new QTreeWidgetItem(QStringList()<<"敏捷");
    QTreeWidgetItem * zliItem = new QTreeWidgetItem(QStringList()<<"智力");
    //加载顶层的节点
    ui->treeWidget->addTopLevelItem(liItem);
    ui->treeWidget->addTopLevelItem(minItem);
    ui->treeWidget->addTopLevelItem(zliItem);

    //追加子节点
    QStringList heroL1;
    heroL1 << "刚被猪" << "前排坦克，能在吸收伤害的同时造成可观的范围输出";
    QTreeWidgetItem * l1 = new QTreeWidgetItem(heroL1);
    liItem->addChild(l1);
}

Widget::~Widget()
{
    delete ui;
}
```

输出结果如下：

![image-20250228181421723](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228181421723.png)

## 5.QTableWidget控件

在ui界面添加Table Widget控件

编写代码如下：

```c++
#include "widget.h"
#include "ui_widget.h"

Widget::Widget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::Widget)
{
    ui->setupUi(this);

    //TableWidget控件
    //设置列数3列
    ui->tableWidget->setColumnCount(3);

    //设置水平表头
    ui->tableWidget->setHorizontalHeaderLabels(QStringList()<<"姓名"<<"性别"<<"年龄");

    //设置行数5行
    ui->tableWidget->setRowCount(5);

    //设置正文
    //ui->tableWidget->setItem(0,0,new QTableWidgetItem("亚瑟"));

    QStringList nameList;
    nameList<<"亚瑟"<<"赵云"<<"张飞"<<"关羽"<<"花木兰";

    QList<QString> sexList;
    sexList << "男"<<"男"<<"男"<<"男"<<"女";

    for(int i=0;i<5;i++)
    {
        int col=0;
        ui->tableWidget->setItem(i,col++,new QTableWidgetItem(nameList[i]));
        ui->tableWidget->setItem(i,col++,new QTableWidgetItem(sexList.at(i)));
        //int 转 QString
        ui->tableWidget->setItem(i,col++,new QTableWidgetItem(QString::number(i+18)));
    }
}

Widget::~Widget()
{
    delete ui;
}
```

输出结果如下：

![image-20250228182938062](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250228182938062.png)



## 6.其他常用控件介绍

1.滚动控件:Scroll Area

![image-20250303103543168](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303103543168.png)

2.Tool Box：

插入页和修改按钮名称可在右侧完成

![image-20250303103907421](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303103907421.png)

3.Tab Widget：

插入页和修改按钮名称可在右侧完成

![image-20250303104101329](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303104101329.png)

4.页面切换 Stacked Widget

可以将其他页面放入，达到切换的效果

![image-20250303105719421](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303105719421.png)

代码如下：

```c++
#include "widget.h"
#include "ui_widget.h"

Widget::Widget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::Widget)
{
    ui->setupUi(this);
    //栈控件使用

    //设置默认定位scrollArea
    ui->stackedWidget->setCurrentIndex(0);

    //scrollArea按钮
    connect(ui->btn_scrollArea, &QPushButton::clicked, [=](){
        ui->stackedWidget->setCurrentIndex(0);
    });

    //toolBox按钮
    connect(ui->btn_toolBox, &QPushButton::clicked, [=](){
        ui->stackedWidget->setCurrentIndex(1);
    });

    //tabWidget按钮
    connect(ui->btn_tabWidget, &QPushButton::clicked, [=](){
        ui->stackedWidget->setCurrentIndex(2);
    });
}

Widget::~Widget()
{
    delete ui;
}
```

实现效果：点击按钮切换页面

![image-20250303105756380](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303105756380.png)

5.下拉框功能实现：Combo Box

![image-20250303110701477](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303110701477.png)

代码：

```c++
//下拉框
    ui->comboBox->addItem("奔驰");
    ui->comboBox->addItem("宝马");
    ui->comboBox->addItem("拖拉机");

    //点击按钮，选中拖拉机选项
    connect(ui->btn_select, &QPushButton::clicked, [=](){
        //ui->comboBox->setCurrentIndex(2);
        ui->comboBox->setCurrentText("拖拉机");
    });
```

![image-20250303110738021](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303110738021.png)

点击按钮，下拉框变为拖拉机

6.Label也可以显示图片和动图，导入图片文件后，添加代码即可显示

代码如下：

```c++
#include <QMovie>
//利用QLabel显示图片
    ui->lbl_Image->setPixmap(QPixmap(":/Image/butterfly.png"));

    //利用QLabel显示 gif动态图片
    QMovie * movie = new QMovie(":/Image/mario.gif");
    ui->lbl_Movie->setMovie(movie);
    //播放动图
    movie->start();
```





![image-20250303121648670](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250303121648670.png)



## 7.自定义控件

1.添加新的文件：

![image-20250305145013373](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305145013373.png)

2.选择设计师界面类：

![image-20250305145158428](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305145158428.png)

3.选择空窗口：

![image-20250305145249492](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305145249492.png)

4.起类名，按顺序生成即可：

![image-20250305145347822](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305145347822.png)

5.在自己的ui界面中，可以添加控件：

![image-20250305145549416](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305145549416.png)



在自定义的ui界面中，添加Spin Box控件和Horizontal Slider控件，现在将这两个控件封装为一个控件

此时想在Widget窗口中使用自己创建的这个控件：

1.可以看到，自定义的这个控件属于Widget类型

![image-20250305150550921](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305150550921.png)



2.在widget.ui中，添加一个Widget控件，选择这个控件，右键->提升为

![image-20250305150737897](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305150737897.png)

3.添加并提升：

![image-20250305150841751](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305150841751.png)



4.运行程序后，输出如下：自定义的控件显示在窗口中

![image-20250305150909784](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305150909784.png)

5.由于上面选择了全局包含，所以再次选择提升时，可直接提升为自定义控件：

![image-20250305151102747](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305151102747.png)

6.输出如下：

![image-20250305151127478](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250305151127478.png)

为了达到这两个控件直接的关联，在smallwidget.cpp中添加代码如下：

```c++
#include "smallwidget.h"
#include "ui_smallwidget.h"

SmallWidget::SmallWidget(QWidget *parent)
    : QWidget(parent)
    , ui(new Ui::SmallWidget)
{
    ui->setupUi(this);

    //QSpring移动 QSlider跟着移动
    void(QSpinBox::*spSignal)(int) = &QSpinBox::valueChanged;
    connect(ui->spinBox, spSignal, ui->horizontalSlider, &QSlider::setValue);

    //QSlider滑动 QSpinBox数字跟着改变
    connect(ui->horizontalSlider, &QSlider::valueChanged, ui->spinBox, &QSpinBox::setValue);

}

SmallWidget::~SmallWidget()
{
    delete ui;
}
```

