

# 一.ROS笔记

## 1.ROS常用语句

### 1.1 快捷键：

==Ctrl+Alt+T==

==切换语言： shift+win+空格==

==Visual Studio中编译的快捷键：ctrl+shift+b==

==退出程序：ctrl+c==

==计算图：rqt_graph==

==取消注释：ctrl+/==

==清空终端：ctrl+l==

==导航实现时功能包：gmapping map_server amcl move_base==

==Gazebo仿真时功能包：urdf xacro gazebo_ros、gazebo_ros_control、gazebo_plugins==

==ctrl+f:搜索一样的名字==

### 1.2 测试ROS命令：

1. 命令行1键入:**roscore**
2. 命令行2键入:**rosrun turtlesim turtlesim_node**(此时会弹出图形化界面)
3. 命令行3键入:**rosrun turtlesim turtle_teleop_key**(在3中可以通过上下左右控制2中乌龟的运动)

### 1.3 编写Hello World语句：

#### 	1.创建工作空间并初始化：

```
mkdir -p 自定义空间名称/src
cd 自定义空间名称
catkin_make
```

上述命令，首先会创建一个工作空间以及一个 src 子目录，然后再进入工作空间调用 catkin_make命令编译。

终端输入命令：

```
1) mkdir -p demo01_ws/src
```

在文件的主目录下生产出一个叫demo01——ws的文件夹如图：

![ros1](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230114204551-1673700526737-3.png)

```
2) cd demo01_ws/
```

进入到demo01_ws这个文件下

```
3) catkin_make
```

在demo_01下除了src文件夹，还产生build和devel两个新的文件夹，如图所示：

![ros2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E6%88%AA%E5%9B%BE20230114212847-1673702973343-6.png)

#### 	2.进入src创建ros包并添加依赖

```
cd src
catkin_create_pkg 自定义ROS包名 roscpp rospy std_msgs
```

上述命令，会在工作空间下生成一个功能包，该功能包依赖于 roscpp、rospy 与 std_msgs，其中roscpp是使用C++实现的库，而rospy则是使用python实现的库，std_msgs是标准消息库，创建ROS功能包时，一般都会依赖这三个库实现。

```
1) cd src
```

进入到src文件夹下

```
2) catkin_create_pkg helloworld roscpp rospy std_msgs
```

在src文件夹下创建helloworld文件夹，如图所示：

![ros3](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E6%88%AA%E5%9B%BE20230115153133-1673768749713-17.png)

#### 3.进入ros包的src目录编辑源文件

1）在demo01_ws/src/helloworld/src文件夹下创建C++的源文件，如图所示：

![ros4](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E6%88%AA%E5%9B%BE20230115154923.png)





```c++
//1.包含ros 的头文件
#include "ros/ros.h"
//2.编写 main 函数
int main(int argc,char *argv[])
{
    //3.初始化ros节点
	ros::init(argc,argv,"hello_node");	//对ROS的节点进行初始化
	//4.输出日志
    ROS_INFO("hello world");		//输出字符串函数
    //如果是在VSCode中输出中文不想有乱码，则需要以下函数：
    setlocale(LC_ALL,"");
    return
}
```







ctrl+alt+t唤起终端

ctrl+shift+b执行编译

win+空格切换语言

launch文件需要先保存一下才能继续执行



### 1.4 VScode的使用

1）终端输入命令：

```
mkdir -p demo01_ws/src
```

在文件的主目录下生产出一个叫demo01——ws的文件夹如图：

![ros1](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230114204551-1673700526737-3.png)

2）进入到demo01_ws这个文件下

```
cd demo01_ws/
```

3）在demo_01下除了src文件夹，还产生build和devel两个新的文件夹，如图所示：

![ros2](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E6%88%AA%E5%9B%BE20230114212847-1673702973343-6.png)

```
catkin_make
```



4）此时如果已经进入到demo03_ws，则输入

```c++
code .
```

否则输入

```c++
cd demo01_ws
code .
```

唤起Visual Studio

5）进入到Visual Studio中后，使用快捷键 ctrl + shift + B 调用编译，选择:`catkin_make:build`

可以点击配置设置为默认，修改.vscode/tasks.json 文件

将源文件替换为：

```c++
{
// 有关 tasks.json 格式的文档，请参见
    // https://go.microsoft.com/fwlink/?LinkId=733558
    "version": "2.0.0",
    "tasks": [
        {
            "label": "catkin_make:debug", //代表提示的描述性信息
            "type": "shell",  //可以选择shell或者process,如果是shell代码是在shell里面运行一个命令，如果是process代表作为一个进程来运行
            "command": "catkin_make",//这个是我们需要运行的命令
            "args": [],//如果需要在命令后面加一些后缀，可以写在这里，比如-DCATKIN_WHITELIST_PACKAGES=“pac1;pac2”
            "group": {"kind":"build","isDefault":true},
            "presentation": {
                "reveal": "always"//可选always或者silence，代表是否输出信息
            },
            "problemMatcher": "$msCompile"
        }
    ]
}


```



6）修改完成后，在src目录下进行功能包的创建

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230209161800.png)

点击最下面的Create Catkin Package



7）在输入栏输入以下两条语句：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230209161930.png)

这个是在src目录下创建一个文件夹

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230209161935.png)

这个是添加C++和python等的依赖包文件



8）至此，在最小的src目录下创建新的文件，既可以实现想要的功能

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230209162052.png)



9）编写好文件后进入CMakeLists.txt

找到136行，改成如下所示：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230219134637.png)

```cmake
add_executable(hello_vscode_c src/hello_vscode_c.cpp)
##这一行是生成一个可执行程序，第一个名字可以随意起
target_link_libraries(hello_vscode_c
${catkin_LIBRARIES}
 )
##这一行是生成一个动态链接库，第一个名字要和上一行的名字对齐
```



10）修改完成后，使用ctrl+shitf+b快捷键编译一下，看是否有错误

检查无误后，使用ctrl+alt+t打开终端，输入roscore并回车，启用ros节点

新开一个终端，在当前条件下输入以下语句：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230219140604.png)

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230219140516.png)

第一句是进入到最大的demo03_ws/的文件夹下

第二句话是初始化

第三句话是启动 具体文件夹下的具体工程



## 2.ROS通信机制



### 2.1话题通信



#### 2.1.1 话题通讯的理论模型：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230219132543.jpg)



![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/01%E8%AF%9D%E9%A2%98%E9%80%9A%E4%BF%A1%E6%A8%A1%E5%9E%8B.jpg)

#### 2.1.2 话题通讯的基本操作：

具体操作请看第40集

发布者函数：

```c++
#include "ros/ros.h"
#include "std_msgs/String.h"
#include <sstream>
/*
     发布方实现：
     1.包含头文件
        ROS中文本类型---> std_msgs/String.h
     2.初始化 ROS 节点
     3.创建节点句柄
     4.创建发布者对象
     5.编写发布逻辑并发布数据


*/

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    //2.初始化 ROS 节点
    ros::init(argc,argv,"erGouZi");
    
    //3.创建节点句柄
    ros::NodeHandle nh;

    //4.创建发布者对象
    ros::Publisher pub = nh.advertise<std_msgs::String>("fang",10);

    //5.编写发布逻辑并发布数据
    //要求以 10HZ 的频率发布数据，并且文本后添加编号
    //先创建被发布的消息
    std_msgs::String msg;
    //发布频率
    ros::Rate rate(10);
    //设置编号
    int count = 0 ;
    //编写循环，循环中发布数据
    while(ros::ok())
    {
        count++;
        //实现字符串拼接数字
        std::stringstream ss;
        ss << "hello--->" << count;
        msg.data = ss.str();
        //msg.data = "hello";
        pub.publish(msg);
        //添加日志：
        ROS_INFO("发布的数据是:%s",ss.str().c_str());
        rate.sleep();
        ros::spinOnce();//官方建议，处理回调函数
    }
    return 0;
}
```

订阅方实现：

```c++
#include "ros/ros.h"
#include "std_msgs/String.h"

/*
    订阅方实现：
     1.包含头文件
        ROS中文本类型---> std_msgs/String.h
     2.初始化 ROS 节点
     3.创建节点句柄
     4.创建订阅者对象
     5.处理订阅到的数据
     6.spin()函数
*/

void doMsg(const std_msgs::String::ConstPtr &msg)
{
    //通过msg获取并操作订阅到的数据
    ROS_INFO("翠花订阅的数据：%s",msg->data.c_str());

}

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    //2.初始化 ROS 节点
    ros::init(argc,argv,"cuiHua");
    //3.创建节点句柄
    ros::NodeHandle nh;
    //4.创建订阅者对象
    ros::Subscriber sub = nh.subscribe("fang",10,doMsg);
    //5.处理订阅到的数据
    ros::spin();
    return 0;
}
```

配置CMakeLists.txt文件：

```c++
add_executable(Hello_pub
  src/Hello_pub.cpp
)
add_executable(Hello_sub
  src/Hello_sub.cpp
)

target_link_libraries(Hello_pub
  ${catkin_LIBRARIES}
)
target_link_libraries(Hello_sub
  ${catkin_LIBRARIES}
)

```

补充0:

vscode 中的 main 函数 声明 int main(int argc, char const *argv[]){}，默认生成 argv 被 const 修饰，需要去除该修饰符

补充1:

ros/ros.h No such file or directory .....

检查 CMakeList.txt find_package 出现重复,删除内容少的即可

参考资料:https://answers.ros.org/question/237494/fatal-error-rosrosh-no-such-file-or-directory/

补充2:

find_package 不添加一些包，也可以运行啊， ros.wiki 答案如下

```
You may notice that sometimes your project builds fine even if you did not call find_package with all dependencies. This is because catkin combines all your projects into one, so if an earlier project calls find_package, yours is configured with the same values. But forgetting the call means your project can easily break when built in isolation.
Copy
```

补充3:

订阅时，第一条数据丢失

原因: 发送第一条数据时， publisher 还未在 roscore 注册完毕

解决: 注册后，加入休眠 ros::Duration(3.0).sleep(); 延迟第一条数据的发



启动时先在终端打开roscore

cd 目标文件夹

source以下

rosrun功能包



#### 2.1.3 话题通讯自定义msg

1.定义msg文件：

创建msg文件：

```c++
string name
int32 age
float32 height
```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220130521.png)





2.编辑配置文件：

在package.xml中添加编译依赖与执行依赖

```c++
  <build_depend>message_generation</build_depend>
  <exec_depend>message_runtime</exec_depend>
  <!-- 
  exce_depend 以前对应的是 run_depend 现在非法
  -->

```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220130729.png)

CMakeLists.txt编译 msg 相关配置

```
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
  message_generation
)
# 需要加入 message_generation,必须有 std_msgs

```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220131440.png)

```
## 配置 msg 源文件
add_message_files(
  FILES
  Person.msg
)

```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220131444.png)

```
# 生成消息时依赖于 std_msgs
generate_messages(
  DEPENDENCIES
  std_msgs
)

```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220131446.png)

```
#执行时依赖
catkin_package(
#  INCLUDE_DIRS include
#  LIBRARIES demo02_talker_listener
  CATKIN_DEPENDS roscpp rospy std_msgs message_runtime
#  DEPENDS system_lib
)

```

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220131448.png)





3.编译：

编译完成后，会产生Person.h文件

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220131914.png)

4.vscode配置：

在集成终端中打开：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220133142.png)

在终端内输入pwd，获得到工作目录

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220133145.png)

然后在vscode中添加目录：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230220133305.png)



发布方：

```c++
#include "ros/ros.h"
#include "plumbing_pub_sub/Person.h"

/*
    发布方：发布人的消息
        1.包含头文件
        2.初始化ros节点
        3.创建节点句柄
        4.创建发布者对象
        5.编写发布逻辑，发布数据


*/



int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    ROS_INFO("这是消息的发布方");
    //2.初始化ros节点
    ros::init(argc,argv,"banZhuRen");
    //3.创建节点句柄
    ros::NodeHandle nh;
    //4.创建发布者对象
    ros::Publisher pub = nh.advertise<plumbing_pub_sub::Person>("liaoTian",10);
    //5.编写发布逻辑，发布数据
    //5-1.创建发布的数据
    plumbing_pub_sub::Person person;
    person.name = "张三";
    person.age = 1;
    person.height = 1.73;
    //5-2.设置发布频率
    ros::Rate rate(1);
    //5-3.循环发布数据
    while(ros::ok())
    {
        //修改数据
        person.age += 1;
        //核心，发布数据
        pub.publish(person);
        ROS_INFO("发布的消息：%s,%d,%.2f",person.name.c_str(),person.age,person.height);
        //休眠
        rate.sleep();
        //建议
        ros::spinOnce();
    }
    return 0;
}
```



订阅方：

```c++
#include "ros/ros.h"
#include "plumbing_pub_sub/Person.h"
/*
    订阅方：订阅消息
        1.包含头文件
            #include "plumbing_pub_sub/Person.h"
        2.初始化ros节点
        3.创建节点句柄
        4.创建订阅者对象
        5.处理订阅的数据
        6.调用spin()函数


*/

void doPerson(const plumbing_pub_sub::Person::ConstPtr& person)
{
    ROS_INFO("订阅人的消息：%s,%d,%.2f",person->name.c_str(),person->age,person->height);

}

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    ROS_INFO("订阅方实现");
    //2.初始化ros节点
    ros::init(argc,argv,"jiaZhang");
    //3.创建节点句柄
    ros::NodeHandle nh;
    //4.创建订阅者对象
    ros::Subscriber sub = nh.subscribe("liaoTian",10,doPerson);
    //5.处理订阅的数据;

    //6.使用spin()函数
    ros::spin();
    return 0;
}
```





### 2.2服务通信

#### 2.2.1 服务通信理论模型：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230301122750.jpg)

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/02_%E6%9C%8D%E5%8A%A1%E9%80%9A%E4%BF%A1%E6%A8%A1%E5%9E%8B.jpg)



#### 2.2.2 服务通信自定义srv

http://www.autolabor.com.cn/book/ROSTutorials/

1.创建srv文件夹，并在srv文件夹下创建srv文件

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120011.png)

2.编辑配置文件

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120117.png)

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120328.png)

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120331.png)

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120333.png)

#### 2.2.3 服务通信自定义srv调用



0.VScode配置：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222120613.png)



```c++
{
    "configurations": [
        {
            "browse": {
                "databaseFilename": "",
                "limitSymbolsToIncludedHeaders": true
            },
            "includePath": [
                "/opt/ros/noetic/include/**",
                "/usr/include/**",
                "/xxx/yyy工作空间/devel/include/**" //配置 head 文件的路径 
            ],
            "name": "ROS",
            "intelliSenseMode": "gcc-x64",
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c11",
            "cppStandard": "c++17"
        }
    ],
    "version": 4
}

```



1.服务端：

```c++
#include "ros/ros.h"
#include "plumbing_server_client/Addints.h"

/*
    服务端实现：解析客户端提交的数据，并运算产生响应
        1.包含头文件
        2.初始化ROS节点；
        3.创建节点句柄
        4。创建服务对象
        5.处理请求并产生响应
        6.spin（)


*/

bool doNums(plumbing_server_client::Addints::Request &request,
            plumbing_server_client::Addints::Response &response)
{
    //1.处理请求
    int num1 = request.num1;
    int num2 = request.num2;
    ROS_INFO("收到的请求数据:num1 = %d,num2 = %d",num1,num2);
    //2.组织响应
    int sum = num1 + num2;
    response.sum = sum;
    ROS_INFO("求和结果: sum = %d",sum);
    return true;
}


int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    /* code */
    //2.初始化ROS节点
    ros::init(argc,argv,"heiShui"); //节点名称需要保证唯一
    //3.创建节点句柄
    ros::NodeHandle nh;
    //4.创建一个服务对象
    ros::ServiceServer server = nh.advertiseService("addInts",doNums);
    ROS_INFO("服务器端启动");
    //5.处理请求并产生响应

    //6.spin()
    ros::spin();
    return 0;
}

```

2.配置文件：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222122651.png)

3.客户端：

```c++
#include "ros/ros.h"
#include "plumbing_server_client/Addints.h"
/*
    客户端实现：提交两个整数，并处理响应的结果
        1.包含头文件；
        2.初始化ROS节点
        3.创建节点句柄
        4.创建一个客户端对象
        5.提交请求并处理响应

    实现参数的动态提交：
        1.格式：rosrun xxxxx xxxxx 12 34
        2.节点执行时，需要获取命令中的参数,并组织进request

    问题：
        如果先启动客户端，那么会请求异常
    需求：
        如果县启动客户端，不要直接抛出异常，而是挂起，等服务器启动后，再正常请求
    解决：
        在ROS中内置了相关函数，这些函数可以让客户端启动后挂起，等待服务器启动
        client.waitForExistence();
        ros::service::waitForService("服务话题");
*/

int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    //优化实现，获取命令中参数
    if(argc != 3)
    {
        ROS_INFO("提交的参数个数不对");
        return 1;

    }


    //2.初始化ROS节点
    ros::init(argc,argv,"daBao");
    //3.创建节点句柄
    ros::NodeHandle nh;
    //4.创建一个客户端对象
    ros::ServiceClient client = nh.serviceClient<plumbing_server_client::Addints>("addInts");
    //5.提交请求并处理响应
    plumbing_server_client::Addints ai;
    //5-1.组织请求
    ai.request.num1 = atoi(argv[1]);
    ai.request.num2 = atoi(argv[2]);
    //5-2.处理响应
    //调用判断服务器状态的函数
    //函数1
    //client.waitForExistence();
    ros::service::waitForService("addInts");
    bool flag = client.call(ai);
    if(flag)
    {
        ROS_INFO("响应成功");
        //响应结果
        ROS_INFO("响应结果 = %d",ai.response.sum);
    }
    else
    {
        ROS_INFO("响应失败");
    }
    /* code */
    return 0;
}
```

4.配置文件：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222122651-1677042650828-23.png)





### 2.3参数服务器通信

#### 2.3.1 参数服务器理论模型

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230222135628.png)



#### 2.3.2 参数操作

实现参数服务器参数的增删改查操作

在C++中实现参数服务器数据的增删改查，可以通过两套 API 实现:

1) ros::NodeHandle
2) ros::param





1.参数服务器新增（修改）参数：

```c++
#include "ros/ros.h"
/*
    需要实现参数的新增与修改
    需求：首先设置机器人的共享参数，类型，半径(0.15m)
        再修改半径(0.2m)
    实现：
        ros::NodeHandle
            setParam("健"，值)
        ros::param
            set("健",值)
    修改，只需要继续调研 setParam 或 set 函数，保证健是已经存在的,那么值会覆盖。

*/


int main(int argc, char *argv[])
{
    /* code */
    //初始化ROS节点
    ros::init(argc,argv,"set_param_c");
    //创建ROS节点句柄
    ros::NodeHandle nh;
    //参数增------
    //方案1：nh
    nh.setParam("type","xiaoHuang");
    nh.setParam("radius",0.15);

    //方案2：ros::param
    ros::param::set("type_param","xiaoBai");
    ros::param::set("radius_param",0.15);
    //参数改------
    //方案1：nh
    nh.setParam("radius",0.2);
    //方案2：ros::param
    ros::param::set("radius_param",0.25);
    return 0;
}
```





2.参数服务器获取参数：

```c++
#include "ros/ros.h"   

/*
    演示参数查询
    实现：
        ros::NodeHandle

        param(键,默认值) 
            存在，返回对应结果，否则返回默认值

        getParam(键,存储结果的变量)
            存在,返回 true,且将值赋值给参数2
            若果键不存在，那么返回值为 false，且不为参数2赋值

        getParamCached键,存储结果的变量)--提高变量获取效率
            存在,返回 true,且将值赋值给参数2
            若果键不存在，那么返回值为 false，且不为参数2赋值

        getParamNames(std::vector<std::string>)
            获取所有的键,并存储在参数 vector 中 

        hasParam(键)
            是否包含某个键，存在返回 true，否则返回 false

        searchParam(参数1，参数2)
            搜索键，参数1是被搜索的键，参数2存储搜索结果的变量

    ros::param ----- 与 NodeHandle 类似
*/


int main(int argc, char *argv[])
{
    //设置编码
    setlocale(LC_ALL,"");
    //初始化ROS节点
    ros::init(argc,argv,"get_param_c");
    //创建节点句柄
    ros::NodeHandle nh;
    //ros::NodeHandle
    //1.param
    double radius = nh.param("radius",0.5);
    ROS_INFO("radius = %.2f",radius);
    //2.getParam
    double radius2 = 0.0;
    //bool result = nh.getParam("radius",radius2);
    //3.getParamCached与getParam类似，只是性能上有提升，一般测试下，看不出来
    bool result = nh.getParamCached("radius",radius2);
    if(result)
    {
        ROS_INFO("获取的半径是 : %.2f",radius2);
    }
    else
    {
        ROS_INFO("被查询的变量不存在。");

    }
    //4.getParamNames
    std::vector<std::string> names;
    nh.getParamNames(names);
    for(auto &&name : names)
    {
        ROS_INFO("遍历的元素:%s",name.c_str());
    }
    //5.hasParam
    bool flag1 = nh.hasParam("radius");
    bool flag2 = nh.hasParam("radiusxxx");
    ROS_INFO("radius 存在吗？ %d",flag1);
    ROS_INFO("radiusxxx 存在吗？ %d",flag2);
    //6.searchParam
    std::string key;
    nh.searchParam("radius",key);
    ROS_INFO("搜索结果:%s",key.c_str());
    //ros::param
    double radius_param = ros::param::param("radius",100.5);
    ROS_INFO("radius_param = %.2f",radius_param);
    std::vector<std::string> names_param;
    ros::param::getParamNames(names_param);
    for(auto &&name : names_param)
    {
        ROS_INFO("健:%s",name.c_str());
    }
    return 0;
}

```





3.参数服务器删除参数

```c++
#include "ros/ros.h"

/*
    演示参数删除：
    实现：
        ros::NodeHandle
            deleteParam()
        ros::param()
            del()
*/
int main(int argc, char *argv[])
{
    setlocale(LC_ALL,"");
    ros::init(argc,argv,"param_del_c");
    ros::NodeHandle nh;

    //删除：NodeHandle
    bool flag1 = nh.deleteParam("radius");
    if(flag1)
    {
        ROS_INFO("删除成功！");
    }
    else
    {
        ROS_INFO("删除失败! ");
    }
    //删除：ros::param
    bool flag2 = ros::param::del("radius_param");
    if(flag2)
    {
        ROS_INFO("radius_param,删除成功！");
    }
    else
    {
        ROS_INFO("radius_param,删除失败! ");
    }
    return 0;
}
```





### 2.4 常用命令

在 ROS 同提供了一些实用的命令行工具，可以用于获取不同节点的各类信息，常用的命令如下:

- rosnode : 操作节点
- rostopic : 操作话题
- rosservice : 操作服务
- rosmsg : 操作msg消息
- rossrv : 操作srv消息
- rosparam : 操作参数





#### 2.4.1rosnode

rosnode是用于获取节点信息的命令

```c++
rosnode ping    测试到节点的连接状态
rosnode list    列出活动节点
rosnode info    打印节点信息
rosnode machine    列出指定设备上节点
rosnode kill    杀死某个节点
rosnode cleanup    清除不可连接的节点
```

#### 2.4.2 rostopic

```c++
rostopic bw     显示主题使用的带宽
rostopic delay  显示带有 header 的主题延迟
rostopic echo   打印消息到屏幕
rostopic find   根据类型查找主题
rostopic hz     显示主题的发布频率
rostopic info   显示主题相关信息
rostopic list   显示所有活动状态下的主题
rostopic pub    将数据发布到主题
rostopic type   打印主题类型
```





#### 2.4.3 rosservice

```c++
rosservice args 打印服务参数
rosservice call    使用提供的参数调用服务
rosservice find    按照服务类型查找服务
rosservice info    打印有关服务的信息
rosservice list    列出所有活动的服务
rosservice type    打印服务类型
rosservice uri    打印服务的 ROSRPC uri
```





#### 2.4.4 rosmsg

```c++
rosmsg show    显示消息描述
rosmsg info    显示消息信息
rosmsg list    列出所有消息
rosmsg md5    显示 md5 加密后的消息
rosmsg package    显示某个功能包下的所有消息
rosmsg packages    列出包含消息的功能包
```





#### 2.4.5 rossrv

```c++
rossrv show    显示服务消息详情
rossrv info    显示服务消息相关信息
rossrv list    列出所有服务信息
rossrv md5    显示 md5 加密后的服务消息
rossrv package    显示某个包下所有服务消息
rossrv packages    显示包含服务消息的所有包
```





#### 2.4.6 rosparam

```c++
rosparam set    设置参数
rosparam get    获取参数
rosparam load    从外部文件加载参数
rosparam dump    将参数写出到外部文件
rosparam delete    删除参数
rosparam list    列出所有参数
```

### 2.5实操

```
#include "ros/ros.h"
#include "geometry_msgs/Twist.h"

/*
    需求：发布速度消息
        话题：/turtlel/cmd_vel
        消息：geometry_msgs/Twist
    
    1.包含头文件
    2.初始化ros节点
    3.创建节点句柄
    4.创建发布对象
    5.发布逻辑
    6.spinOnce();



*/

int main(int argc, char *argv[])
{
    /* code */
    //2.初始化ROS节点
    ros::init(argc,argv,"my_control");

    //3.创建节点句柄
    ros::NodeHandle nh;

    //4.创建发布对象
    ros::Publisher pub = nh.advertise<geometry_msgs::Twist>("/turtlel/cmd_vel",10);

    //5.发布逻辑
    ros::Rate rate(10); //设置发布频率

    //组织被发布的消息
    geometry_msgs::Twist twist;
    twist.linear.x=1.0;
    twist.linear.y=0.0;
    twist.linear.z=0.0;

    twist.angular.x=0.0;
    twist.angular.y=0.0;
    twist.angular.z=0.5;

    while(ros::ok())
    {
        pub.publish(twist);
        //休眠
        rate.sleep();
        //回头
        ros::spinOnce();

    }
    return 0;
}
```







## 4.ROS运行管理



### 4.2 ROS节点管理launch文件

1.新建launch文件：

右键src，创建新的功能包，在功能包内添加roscpp rospy std_msgs turtlesim

2.在src目录下创建launch_basic文件夹，文件夹下创建launch文件

```xml
<launch>
    <!-- 启动的节点-->
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen" />
    <!--键盘控制节点-->
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
</launch>
```

注意：1.launch文件写完后要保存才可以执行

​			2.roslaunch 命令执行launch文件时，首先会判断是否启动了 roscore,如果启动了，则不再启动，否则，会自动调用 roscore

执行语句：

```xml
source ./devel/setup.bash
roslaunch launch01_basic start_turtle.launch
```





#### 4.2.1 launch文件标签之launch

`<launch>`标签是所有 launch 文件的根标签，充当其他标签的容器

**属性：**deprecated = "弃用声明"`

告知用户当前 launch 文件已经弃用，在第一行launch语句中添加

**子级标签：**所有其它标签都是launch的子级



#### 4.2.2 launch文件标签之node

`<node>`标签用于指定 ROS 节点，是最常见的标签，需要注意的是: roslaunch 命令不能保证按照 node 的声明顺序来启动节点(节点的启动是多进程的)

**属性：**

- pkg="包名"

  节点所属的包

- type="nodeType"

  节点类型(与之相同名称的可执行文件)

- name="nodeName"

  节点名称(在 ROS 网络拓扑中节点的名称)

- args="xxx xxx xxx" (可选)

  将参数传递给节点

- machine="机器名"

  在指定机器上启动节点

- respawn="true | false" (可选)

  如果节点退出，是否自动重启

- respawn_delay=" N" (可选)

  如果 respawn 为 true, 那么延迟 N 秒后启动节点

- required="true | false" (可选)

  该节点是否必须，如果为 true,那么如果该节点退出，将杀死整个 roslaunch

- ns="xxx" (可选)

  在指定命名空间 xxx 中启动节点

- clear_params="true | false" (可选)

  在启动前，删除节点的私有空间的所有参数

- output="log | screen" (可选)

  日志发送目标，可以设置为 log 日志文件，或 screen 屏幕,默认是 log



**子级标签：**

- env 环境变量设置
- remap 重映射节点名称
- rosparam 参数设置
- param 参数设置

#### 4.2.3 launch文件标签之include

`include`标签用于将另一个 xml 格式的 launch 文件导入到当前文件

**属性：**

- file="$(find 包名)/xxx/xxx.launch"

  要包含的文件路径

- ns="xxx" (可选)

  在指定命名空间导入文件

**子级标签：**

- env 环境变量设置
- arg 将参数传递给被包含的文件

代码：

```xml
<!--需要复用 start_turtle.launch-->

<launch>
    <include file="$(find launch01_basic)/launch/start_turtle.launch" />
    <!--其他节点-->
</launch>
```



#### 4.2.4 launch文件标签之remap

用于话题重命名

**属性：**

- from="xxx"

  原始话题名称

- to="yyy"

  目标名称

**子级标签：**

无

```xml
<launch>
    <!-- 启动的节点-->
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen">
        <remap from="/turtlel/cmd_vel" to="/cmd_vel" />
    </node>
    <!--键盘控制节点-->
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
</launch>
```



#### 4.2.5 launch文件标签之param



`<param>`标签主要用于在参数服务器上设置参数，参数源可以在标签中通过 value 指定，也可以通过外部文件加载，在`<node>`标签中时，相当于私有命名空间。



**属性：**

- name="命名空间/参数名"

  参数名称，可以包含命名空间

- value="xxx" (可选)

  定义参数值，如果此处省略，必须指定外部文件作为参数源

- type="str | int | double | bool | yaml" (可选)

  指定参数类型，如果未指定，roslaunch 会尝试确定参数类型，规则如下:

  - 如果包含 '.' 的数字解析未浮点型，否则为整型
  - "true" 和 "false" 是 bool 值(不区分大小写)
  - 其他是字符串

**子级标签：**

无

代码：

```xml
<launch>
     <!--格式1：launch下，node外-->
     <param name="param_A" type="int" value="100" />
     <!-- 启动的节点-->
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen">
        <remap from="/turtlel/cmd_vel" to="/cmd_vel" />
        <!--格式2：node下-->
        <param name="param_B" type="double" value="3.14" />
    </node>
    <!--键盘控制节点-->
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
   
</launch>
```



![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230225110238.png)



#### 4.2.6 launch文件标签之rosparam

`<rosparam>`标签可以从 YAML 文件导入参数，或将参数导出到 YAML 文件，也可以用来删除参数，`<rosparam>`标签在`<node>`标签中时被视为私有

**属性：**

- command="load | dump | delete" (可选，默认 load)

  加载、导出或删除参数

- file="$(find xxxxx)/xxx/yyy...."

  加载或导出到的 yaml 文件

- param="参数名称"

- ns="命名空间" (可选)

**子级标签：**

无

代码1：

```xml
<launch>
    <!--param使用：向参数服务器设置参数-->
     <!--格式1：launch下，node外-->
     <param name="param_A" type="int" value="100" />

     <!--rosparam 使用: 操作参数服务器数据-->
    <!--格式1：launch下，node外-->
    <!--加载参数-->
    <rosparam command="load" file="$(find launch01_basic)/launch/params.yaml" />
    <!--导出参数-->
    
     <!-- 启动的节点-->
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen">
        <remap from="/turtlel/cmd_vel" to="/cmd_vel" />
        <!--格式2：node下-->
        <param name="param_B" type="double" value="3.14" />
        <!--格式2：node下-->
        <rosparam command="load" file="$(find launch01_basic)/launch/params.yaml" />
    </node>
    <!--键盘控制节点-->
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
   
</launch>
```



代码2：

```xml
<launch>

    <rosparam command="dump" file="$(find launch01_basic)/launch/params_out.yaml" />
    <!--删除参数-->
    <rosparam command="delete" param="bg_B" />
</launch>
```



注意：1.定义yaml文件时，要有空格

​			2.当运行的是delete指令时，最好新开一个窗口实现。





#### 4.2.7 launch文件标签之group

`<group>`标签可以对节点分组，具有 ns 属性，可以让节点归属某个命名空间



**属性：**

- ns="名称空间" (可选)

- clear_params="true | false" (可选)

  启动前，是否删除组名称空间的所有参数(慎用....此功能危险

**子级标签：**

- 除了launch 标签外的其他标签

示例：

```xml
<launch>
    <!--启动两对乌龟 与 键盘控制节点-->

<group ns="first">
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen" />
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
</group>

<group ns="second">
    <node pkg="turtlesim" type="turtlesim_node" name="my_turtle" output="screen" />
    <node pkg="turtlesim" type="turtle_teleop_key" name="my_key" output="screen" />
</group>

</launch>
```



#### 4.2.8 launch文件标签之arg

`<arg>`标签是用于动态传参，类似于函数的参数，可以增强launch文件的灵活性

**属性：**

- name="参数名称"

- default="默认值" (可选)

- value="数值" (可选)

  不可以与 default 并存

- doc="描述"

  参数说明

**子级标签：**

无

代码：

```xml
<launch>
    <!--需求：演示arg的使用，需要设置多个参数，这些参数使用的是同一个值（小车的产度）,怎么设置？-->
    <!--<param name="A" value="0.55" />
    <param name="B" value="0.55" />
    <param name="C" value="0.55" />-->

    <arg name="car_length" default="0.5" />
    <param name="A" value="$(arg car_length)" />
    <param name="B" value="$(arg car_length)" />
    <param name="C" value="$(arg car_length)" />
</launch>
```



也可以在启动launch文件的时候改变小车的数值：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230225110238-1677301502233-2.png)

## 6. 机器人系统仿真

### 6.1URDF集成Rviz基本流程：



**实现流程：**

1. 准备:新建功能包，导入依赖
2. 核心:编写 urdf 文件
3. 核心:在 launch 文件集成 URDF 与 Rviz
4. 在 Rviz 中显示机器人模型



**1.新建功能包，导入依赖**

创建一个新的功能包，名称自定义，导入依赖包:`urdf`与`xacro`

在当前功能包下，再新建几个目录:

`urdf`: 存储 urdf 文件的目录

`meshes`:机器人模型渲染文件(暂不使用)

`config`: 配置文件

`launch`: 存储 launch 启动文件

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230223200317.png)



**2.编写 URDF 文件**

URDF代码：

```xml
<robot name="mycar">
    <link name="base_link">
        <visual>
            <geometry>
                <box size="0.5 0.2 0.1" />
            </geometry>
        </visual>
    </link>
</robot>

```



**3.在 launch 文件中集成 URDF 与 Rviz**

在`launch`目录下，新建一个 launch 文件，该 launch 文件需要启动 Rviz，并导入 urdf 文件，Rviz 启动后可以自动载入解析`urdf`文件，并显示机器人模型，核心问题:如何导入 urdf 文件? 在 ROS 中，可以将 urdf 文件的路径设置到参数服务器，使用的参数名是:`robot_description`,示例代码如下:

```xml
<launch>

    <!-- 设置参数 -->
    <param name="robot_description" textfile="$(find 包名)/urdf/urdf/urdf01_HelloWorld.urdf" />

    <!-- 启动 rviz -->
    <node pkg="rviz" type="rviz" name="rviz" />

</launch>

```



4.在 Rviz 中显示机器人模型

终端输入：

```
roslaunch urdf01_rviz demo01_heloworld.launch
```

rviz 启动后，会发现并没有盒装的机器人模型，这是因为默认情况下没有添加机器人显示组件，需要手动添加，添加方式如下:![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/01_URDF%E6%96%87%E4%BB%B6%E6%89%A7%E8%A1%8Crviz%E9%85%8D%E7%BD%AE01.png)![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/02_URDF%E6%96%87%E4%BB%B6%E6%89%A7%E8%A1%8Crviz%E9%85%8D%E7%BD%AE02.png)设置完毕后，可以正常显示了

5. 优化 Rviz 启动：

重复启动`launch`文件时，Rviz 之前的组件配置信息不会自动保存，需要重复执行步骤4的操作，为了方便使用，可以使用如下方式优化:

首先，将当前配置保存进`config`目录![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/10_rviz%E9%85%8D%E7%BD%AE%E4%BF%9D%E5%AD%98.png)

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230225133731.png)

然后，`launch`文件中 Rviz 的启动配置添加参数:`args`,值设置为`-d 配置文件路径`

```xml
<launch>
    <!-- 设置参数 -->
    <param name="robot_description" textfile="$(find urdf01_rviz)/urdf/urdf/demo01_helloworld.urdf" />
    <!-- 启动 rviz -->
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz"/>
</launch>
```





### 6.2 URDF语法详解

URDF 文件是一个标准的 XML 文件，在 ROS 中预定义了一系列的标签用于描述机器人模型，机器人模型可能较为复杂，但是 ROS 的 URDF 中机器人的组成却是较为简单，可以主要简化为两部分:连杆(link标签) 与 关节(joint标签)，接下来我们就通过案例了解一下 URDF 中的不同标签:

- robot 根标签，类似于 launch文件中的launch标签
- link 连杆标签
- joint 关节标签
- gazebo 集成gazebo需要使用的标签

##### 6.2.1 URDF语法详解01_robot

urdf 中为了保证 xml 语法的完整性，使用了`robot`标签作为根标签，所有的 link 和 joint 以及其他标签都必须包含在 robot 标签内,在该标签内可以通过 name 属性设置机器人模型的名称

**1.属性**

name: 指定机器人模型的名称

**2.子标签**

其他标签都是子级标签

##### 6.2.2 URDF语法详解02_link

**link**

urdf 中的 link 标签用于描述机器人某个部件(也即刚体部分)的外观和物理属性，比如: 机器人底座、轮子、激光雷达、摄像头...每一个部件都对应一个 link, 在 link 标签内，可以设计该部件的形状、尺寸、颜色、惯性矩阵、碰撞参数等一系列属性![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E5%AE%98%E6%96%B901_link.png)

**1.属性**

- name ---> 为连杆命名

**2.子标签**

- visual ---> 描述外观(对应的数据是可视的)
  - geometry 设置连杆的形状
    - 标签1: box(盒状)
      - 属性:size=长(x) 宽(y) 高(z)
    - 标签2: cylinder(圆柱)
      - 属性:radius=半径 length=高度
    - 标签3: sphere(球体)
      - 属性:radius=半径
    - 标签4: mesh(为连杆添加皮肤)
      - 属性: filename=资源路径(格式:**package://<packagename>/<path>/文件**)
  - origin 设置偏移量与倾斜弧度
    - 属性1: xyz=x偏移 y便宜 z偏移
    - 属性2: rpy=x翻滚 y俯仰 z偏航 (单位是弧度)
  - material 设置材料属性(颜色)
    - 属性: name
    - 标签: color
      - 属性: rgba=红绿蓝权重值与透明度 (每个权重值以及透明度取值[0,1])
- collision ---> 连杆的碰撞属性
- Inertial ---> 连杆的惯性矩阵

代码实现：

```xml
<!--需求：设置不同形状的机器人部件-->

<robot name="mycar">
    <link name="base_link">
        <!--可视化标签-->
        <visual>
            <!--1.形状-->
            <geometry>
            <!--1.1立方体-->
            <!-- <box size="0.3 0.2 0.1" /> -->
            <!--1.2圆柱-->
            <!--<cylinder radius="0.1" length="2" />-->
            <!--1.3球体-->
            <!--<sphere radius="1" />-->
            <!--1.4皮肤-->
            <mesh filename="package://urdf01_rviz/meshes/autolabor_mini.stl"/>
            </geometry>
            <!--2.偏移量与倾斜弧度-->
            <!--
                    xyz 设置机器人模型在x y z 上的偏移量
                    rpy 用于设置倾斜弧度 x(翻滚) y(俯仰) z(偏航)
            -->
            <origin xyz="0 0 0" rpy="1.57 0 1.57" />

​            <!--3.颜色-->
​            <!--
​                rgba:
​                    r = red
​                    g = green
​                    b = blue
​                    a = 透明度
​                    四者取值[0,1]
​            -->
​            <material name="car_color">
​                <color rgba="0.5 0.2 1 0.4" />
​            </material>
​        </visual>
​    </link>
</robot>
```



launch文件：

```xml
<launch>
    <!-- 设置参数 -->
    <param name="robot_description" textfile="$(find urdf01_rviz)/urdf/urdf/demo02_link.urdf" />
    <!-- 启动 rviz -->
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz"/>
</launch>
```

注意：==第一行里的文件要改成demo02_link，不要用demo01或其他文件==

在使用mesh时，要先把将要使用的文件复制到demo05_ws/下面的meshes文件夹下：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230225194050.png)

注意：1.在使用没有标签的函数时，要在句末加上/

​			2.若使用有标签的函数，注意函数内部要先定义名字，标签内部要有/





##### 6.2.3 URDF语法详解03_joint

**joint**

urdf 中的 joint 标签用于描述机器人关节的运动学和动力学属性，还可以指定关节运动的安全极限，机器人的两个部件(分别称之为 parent link 与 child link)以"关节"的形式相连接，不同的关节有不同的运动形式: 旋转、滑动、固定、旋转速度、旋转角度限制....,比如:安装在底座上的轮子可以360度旋转，而摄像头则可能是完全固定在底座上。

joint标签对应的数据在模型中是不可见的![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E5%AE%98%E6%96%B902_link.png)

**1.属性**

- name ---> 为关节命名
- type ---> 关节运动形式
  - continuous: 旋转关节，可以绕单轴无限旋转
  - revolute: 旋转关节，类似于 continues,但是有旋转角度限制
  - prismatic: 滑动关节，沿某一轴线移动的关节，有位置极限
  - planer: 平面关节，允许在平面正交方向上平移或旋转
  - floating: 浮动关节，允许进行平移、旋转运动
  - fixed: 固定关节，不允许运动的特殊关节

**2.子标签**

- parent(必需的)

  parent link的名字是一个强制的属性：

  - link:父级连杆的名字，是这个link在机器人结构树中的名字。

- child(必需的)

  child link的名字是一个强制的属性：

  - link:子级连杆的名字，是这个link在机器人结构树中的名字。

- origin

  - 属性: xyz=各轴线上的偏移量 rpy=各轴线上的偏移弧度。

- axis

  - 属性: xyz用于设置围绕哪个关节轴运动。



代码实现：

```xml
<!--需求：设置机器人底盘，并添加摄像头-->

<robot name="mycar">
    <!--1.底盘link-->
    <link name="base_link">
        <visual>
            <geometry>
            <box size="0.3 0.2 0.1" /> 
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="car_color">
                <color rgba="0.8 0.5 0 0.5" />
            </material>
        </visual>
    </link>
    <!--2.摄像头link-->
    <link name="camera">
        <visual>
            <geometry>
            <box size="0.02 0.05 0.05" /> 
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="camera_color">
                <color rgba="0 0 1 0.5" />
            </material>
        </visual>
    </link>

<!--发布-->

<joint name="camera2baselink" type="continuous">
    <!--父级标签-->
    <parent link="base_link" />
    <!--子级标签-->
    <child link="camera" />
    <!--设置偏移量-->
    <origin xyz="0.12 0 0.15" rqy="0 0 0" />
    <!--关节旋转参考的坐标轴-->
    <axis xyz="0 0 1" />
</joint>
</robot>
```



使用base_footprint优化URDF

```xml
<robot name="mycar">
    <link name="base_footprint">
        <visual>
            <geometry>
            <box size="0.001 0.001 0.001" /> 
            </geometry>
        </visual>
    </link>

    <link name="base_link">
        <visual>
            <geometry>
            <box size="0.3 0.2 0.1" /> 
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="car_color">
                <color rgba="0.8 0.5 0 0.5" />
            </material>
        </visual>
    </link>
    <link name="camera">
        <visual>
            <geometry>
            <box size="0.02 0.05 0.05" /> 
            </geometry>
            <origin xyz="0 0 0.025" rpy="0 0 0" />
            <material name="camera_color">
                <color rgba="0 0 1 0.5" />
            </material>
        </visual>
    </link>

<joint name="link2footprint" type="fixed">
    <parent link="base_footprint" />
    <child link="base_link" />
    <origin xyz="0 0 0.05" rqy="0 0 0" />
</joint>

<joint name="camera2baselink" type="continuous">
    <parent link="base_link" />
    <child link="camera" />
    <origin xyz="0.12 0 0.05" rqy="0 0 0" />
    <axis xyz="0 0 1" />
</joint>
</robot>
```

joint的launch文件编写：

```xml
<launch>
    <!-- 设置参数 -->
    <param name="robot_description" textfile="$(find urdf01_rviz)/urdf/urdf/demo03_joint.urdf" />
    <!-- 启动 rviz -->
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz"/>
    <!--
        只有上述两条语句：
            表现：摄像头显示位置与颜色异常
            提示：No transform from [camera] to [base_link] 缺少camera到base_link的坐标变换
            原因：rviz中显示 URDF时，必须发布不同部件之间的 坐标系关系
            解决：ROS中提供了关于机器人模型显示的坐标发布相关节点(两个)
    -->

    <!--关节状态发布节点-->
    <node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher" />
    <!--机器人状态发布节点-->
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" />
    <!--添加控制关节运动节点-->
    <node pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" name="joint_state_publisher_gui" />
</launch>
```

注意：1.==第一行的文件名要修改==

​			2.使用joint_state_publisher函数时，==URDF文件内不可以有中文==

​			3.控制关节运动节点这一行可以不写

##### 6.2.4 URDF练习



注意：1.base_link与base_footprint之间的偏移量是==通过joint来实现的==，不要通过link来实现。

​			2.base_link与base_footprint之间的距离一般是半个base_link的长度。



```xml
<robot name="mycar">
    <link name="base_footprint">
        <visual>
            <geometry>
                <sphere radius="0.001"/>
            </geometry>
        </visual>
    </link>

    <link name="base_link">
        <visual>
            <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="baselink_color">
                <color rgba="1.0 0.5 0.2 0.5" />
            </material>
        </visual>
    </link>

    <link name="left_wheel">
        <visual>
            <geometry>
                <cylinder radius="0.0325" length="0.015" />
            </geometry>
            <origin xyz="0 0 0" rpy="1.5705 0 0" />
            <material name="wheel_color">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>
    </link>

    <link name="right_wheel">
        <visual>
            <geometry>
                <cylinder radius="0.0325" length="0.015" />
            </geometry>
            <origin xyz="0 0 0" rpy="1.5705 0 0" />
            <material name="wheel_color">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>
    </link>

    <joint name="link2footprint" type="fixed">
        <parent link="base_footprint" />
        <child link="base_link" />
        <origin xyz="0 0 0.055" rpy="0 0 0" />
    </joint>

    <joint name="left2base_link" type="continuous">
        <parent link="base_link" />
        <child link="left_wheel" />
        <origin xyz="0 0.1 -0.0225" rpy="0 0 0" />
        <axis xyx="0 1 0" />
    </joint>

    <joint name="right2base_link" type="continuous">
        <parent link="base_link" />
        <child link="right_wheel" />
        <origin xyz="0 -0.1 -0.0225" rpy="0 0 0" />
        <axis xyx="0 1 0" />
    </joint>

</robot>
```



```xml
<robot name="mycar">
    <link name="base_footprint">
        <visual>
            <geometry>
                <sphere radius="0.001" />
            </geometry>
        </visual>
    </link>
    <link name="base_link">
        <visual>
            <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="yellow">
                <color rgba="0.8 0.3 0.1 0.5" />
            </material>
        </visual>
    </link>

    <joint name="base_link2base_footprint" type="fixed">
        <parent link="base_footprint" />
        <child link="base_link"/>
        <origin xyz="0 0 0.055" />
    </joint>
    
    <link name="left_wheel">
        <visual>
            <geometry>
                <cylinder radius="0.0325" length="0.015" />
            </geometry>
            <origin xyz="0 0 0" rpy="1.5705 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>

    </link>

    <joint name="left_wheel2base_link" type="continuous">
        <parent link="base_link" />
        <child link="left_wheel" />
        <origin xyz="0 0.1 -0.0225" />
        <axis xyz="0 1 0" />
    </joint>


    <link name="right_wheel">
        <visual>
            <geometry>
                <cylinder radius="0.0325" length="0.015" />
            </geometry>
            <origin xyz="0 0 0" rpy="1.5705 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>

    </link>

    <joint name="right_wheel2base_link" type="continuous">
        <parent link="base_link" />
        <child link="right_wheel" />
        <origin xyz="0 -0.1 -0.0225" />
        <axis xyz="0 1 0" />
    </joint>


</robot>
```



##### 6.2.5 URDF工具

在 ROS 中，提供了一些工具来方便 URDF 文件的编写，比如:

- `check_urdf`命令可以检查复杂的 urdf 文件是否存在语法问题
- `urdf_to_graphiz`命令可以查看 urdf 模型结构，显示不同 link 的层级关系

当然，要使用工具之前，首先需要安装，安装命令:`sudo apt install liburdfdom-tools`

**1.check_urdf 语法检查**

进入urdf文件所属目录，调用:`check_urdf urdf文件`，如果不抛出异常，说明文件合法,否则非法

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/03_URDF%E6%96%87%E4%BB%B6%E6%A3%80%E6%9F%A5_%E6%AD%A3%E5%B8%B8.png)

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/04_URDF%E6%96%87%E4%BB%B6%E6%A3%80%E6%9F%A5_%E5%BC%82%E5%B8%B8.png)

**2.urdf_to_graphiz 结构查看**

进入urdf文件所属目录，调用:`urdf_to_graphiz urdf文件`，当前目录下会生成 pdf 文件

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/05_%E6%9F%A5%E7%9C%8BURDF%E6%96%87%E4%BB%B6%E6%A8%A1%E5%9E%8B%E7%BB%93%E6%9E%84.png)

终端中输入:

```xml
urdf_to_graphiz demo05_test.urdf
evince mycar.pdf
```

即可查看关系

### 6.3 URDF优化_xacro

#### 6.3.1 Xacro_快速体验



**1.Xacro文件编写：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">

    <!--
        上节案例问题：
            1.代码复用  === Xacro宏(函数)
            2.参数设计  === Xacro变量
    -->

    <!-- 属性封装 -->
    <xacro:property name="wheel_radius" value="0.0325" />
    <xacro:property name="wheel_length" value="0.0015" />
    <xacro:property name="PI" value="3.1415927" />
    <xacro:property name="base_link_length" value="0.08" />
    <xacro:property name="lidi_space" value="0.015" />

    <!-- 宏 -->
    <xacro:macro name="wheel_func" params="wheel_name flag" >
        <link name="${wheel_name}_wheel">
            <visual>
                <geometry>
                    <cylinder radius="${wheel_radius}" length="${wheel_length}" />
                </geometry>

                <origin xyz="0 0 0" rpy="${PI / 2} 0 0" />

                <material name="wheel_color">
                    <color rgba="0 0 0 0.3" />
                </material>
            </visual>
        </link>

        <!-- 3-2.joint -->
        <joint name="${wheel_name}2link" type="continuous">
            <parent link="base_link"  />
            <child link="${wheel_name}_wheel" />
            <!-- 
                x 无偏移
                y 车体半径
                z z= 车体高度 / 2 + 离地间距 - 车轮半径

            -->
            <origin xyz="0 ${0.1 * flag} ${(base_link_length / 2 + lidi_space - wheel_radius) * -1}" rpy="0 0 0" />
            <axis xyz="0 1 0" />
        </joint>

    </xacro:macro>

    <!--调用语法-->
    <xacro:wheel_func wheel_name="left" flag="1" />
    <xacro:wheel_func wheel_name="right" flag="-1" />
</robot>
```



**2.Xacro文件转换为urdf文件：**

1）先在终端内输入roscore

2）打开xacro集成终端，输入`rosrun xacro xacro xxx.xacro > xxx.urdf`, 会将 xacro 文件解析为 urdf 文件，

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230226104513.png)

#### 6.3.2 Xacro_语法详解

xacro 提供了可编程接口，类似于计算机语言，包括变量声明调用、函数声明与调用等语法实现。在使用 xacro 生成 urdf 时，根标签`robot`中必须包含命名空间声明:`xmlns:xacro="http://wiki.ros.org/xacro"`



**1.属性与算数运算**

用于封装 URDF 中的一些字段，比如: PAI 值，小车的尺寸，轮子半径 ....

**属性定义**

```xml
<xacro:property name="xxxx" value="yyyy" />
Copy
```

**属性调用**

```
${属性名称}
Copy
```

**算数运算**

```
${数学表达式}
```

示例：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <!--1.属性定义-->
    <xacro:property name="PI" value="3.1415927" />
    <xacro:property name="radius" value="0.03" />
    <!--2.属性调用-->
    <myUsePropertyxxx name="${PI}" />
    <myUsePropertyxxx name="${radius}" />
    <!--3.算术运算-->
    <myUsePropertyxxx result="${PI/2}" />
    <myUsePropertyxxx result="${radius*2}" />
</robot>
```

注意：1.调用和运算中使用的==都是花括号{}==，而不是小括号()

​			2.xacro后面有:

​			3.调用的时候使用的语句是 rosrun xacro xacro demo02_field.urdf.xacro





**2.宏**

类似于函数实现，提高代码复用率，优化代码结构，提高安全性

**宏定义**

```xml
<xacro:macro name="宏名称" params="参数列表(多参数之间使用空格分隔)">

    .....

    参数调用格式: ${参数名}

</xacro:macro>
Copy
```

**宏调用**

```xml
<xacro:宏名称 参数1="xxx" 参数2="xxx"/>
```

示例：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <!--1.宏定义-->
    <xacro:macro name="getSum" params="num1 num2">
        <result value="${num1+num2}" />
    </xacro:macro>
    <!--2.宏调用-->
    <xacro:getSum num1="1" num2="5" />
</robot>
```





**3.文件包含**

机器人由多部件组成，不同部件可能封装为单独的 xacro 文件，最后再将不同的文件集成，组合为完整机器人，可以使用文件包含实现

**文件包含**

```xml
<robot name="xxx" xmlns:xacro="http://wiki.ros.org/xacro">
      <xacro:include filename="my_base.xacro" />
      <xacro:include filename="my_camera.xacro" />
      <xacro:include filename="my_laser.xacro" />
      ....
</robot>
```

示例：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <!--演示文件包含-->
    <xacro:include filename="demo02_field.urdf.xacro" />
    <xacro:include filename="demo03_macro.urdf.xacro" />
</robot>
```



#### 6.3.3 Xacro_完整使用流程示例



**1.编写xacro文件：**



```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">

    <xacro:property name="footprint_radius" value="0.001" />

    <link name="base_footprint">
        <visual>
            <geometry>
                <sphere radius="${footprint_radius}" />
            </geometry>
        </visual>
    </link>

    <xacro:property name="base_radius" value="0.1" />
    <xacro:property name="base_length" value="0.08" />
    <xacro:property name="lidi" value="0.015" />
    <xacro:property name="base_joint_z" value="${base_length / 2 + lidi}" />

    <link name="base_link">
        <visual>
            <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="yellow">
                <color rgba="0.8 0.3 0.1 0.5" />
            </material>
        </visual>
    </link>

    <joint name="base_link2base_footprint" type="fixed">
        <parent link="base_footprint" />
        <child link="base_link"/>
        <origin xyz="0 0 0.055" />
    </joint>


    <xacro:property name="wheel_radius" value="0.0325" />
    <xacro:property name="wheel_length" value="0.015" />
    <xacro:property name="PI" value="3.1415927" />

    <xacro:property name="wheel_joint_z" value="${(base_length/2 + lidi - wheel_radius) * -1}" />

    <xacro:macro name="wheel_func" params="wheel_name flag">
    <link name="${wheel_name}_wheel">
        <visual>
            <geometry>
                <cylinder radius="${wheel_radius}" length="${wheel_length}" />
            </geometry>
            <origin xyz="0 0 0" rpy="${PI / 2} 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>

    </link>

    <joint name="${wheel_name}2base_link" type="continuous">
        <parent link="base_link" />
        <child link="${wheel_name}_wheel" />
        <origin xyz="0 ${0.1 * flag} ${wheel_joint_z}" rpy="0 0 0"/>
        <axis xyz="0 1 0" />
    </joint>
    </xacro:macro>

    <xacro:wheel_func wheel_name="left" flag="1" />
    <xacro:wheel_func wheel_name="right" flag="-1" />


    <xacro:property name="small_wheel_radius" value="0.0075" />
    <xacro:property name="small_joint_z" value="${(base_length / 2 + lidi -small_wheel_radius) * -1}" />

    <xacro:macro name="small_wheel_func" params="small_wheel_name flag">
    <link name="${small_wheel_name}_wheel">
        <visual>
            <geometry>
                <sphere radius="${small_wheel_radius}" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>
    </link>

    <joint name="${small_wheel_name}2base_link" type="continuous">
        <parent link="base_link" />
        <child link="${small_wheel_name}_wheel" />
        <origin xyz="${0.08 * flag} 0 ${small_joint_z}" />
        <axis xyz="1 1 1" />
    </joint>
    </xacro:macro>

    <xacro:small_wheel_func small_wheel_name="front" flag="1" />
    <xacro:small_wheel_func small_wheel_name="back" flag="-1" />
</robot>
```



**2.集成launch文件**

**方式1:**先将 xacro 文件转换出 urdf 文件，然后集成

先将 xacro 文件解析成 urdf 文件:`rosrun xacro xacro xxx.xacro > xxx.urdf`然后再按照之前的集成方式直接整合 launch 文件,内容示例:

```xml
<launch>
    <param name="robot_description" textfile="$(find urdf01_rviz)/urdf/urdf/demo05_test.urdf" />
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz"/>
    <node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher" />
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" />
    <node pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" name="joint_state_publisher_gui" />
</launch>
```

**方式2:**在 launch 文件中直接加载 xacro(**建议使用**)

launch 内容示例:

```xml
<launch>
    <param name="robot_description" command="$(find xacro)/xacro $(find urdf01_rviz)/urdf/xacro/demo05_car_base.urdf.xacro" />

    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz" />
    <node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher" output="screen" />
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" output="screen" />
    <node pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" name="joint_state_publisher_gui" output="screen" />

</launch>
```

核心代码:

```xml
<param name="robot_description" command="$(find xacro)/xacro $(find demo01_urdf_helloworld)/urdf/xacro/my_base.urdf.xacro" />
Copy
```

注意：1.加载`robot_description`时==使用command属性==，属性值就是调用 xacro 功能包的 xacro 程序直接解析 xacro 文件。

​			2.launch文件中找文件夹是小括号==()==，xacro文件中找参数是花括号=={}==

#### 6.3.4 Xacro_实操

**需求描述:**

在前面小车底盘基础之上，添加摄像头和雷达传感器。

**结果演示:**

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/17_xacro%E6%A1%88%E4%BE%8B.png)

**实现分析:**

机器人模型由多部件组成，可以将不同组件设置进单独文件，最终通过文件包含实现组件的拼装。

**实现流程:**

1. 首先编写摄像头和雷达的 xacro 文件
2. 然后再编写一个组合文件，组合底盘、摄像头与雷达
3. 最后，通过 launch 文件启动 Rviz 并显示模型



1.先编写组合文件：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

</robot>
```



2.编写launch文件：

```xml
<launch>
    <param name="robot_description" command="$(find xacro)/xacro $(find urdf01_rviz)/urdf/xacro/car.urdf.xacro" />

    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz" />
    <node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher" output="screen" />
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" output="screen" />
    <node pkg="joint_state_publisher_gui" type="joint_state_publisher_gui" name="joint_state_publisher_gui" output="screen" />

</launch>
```



3.编写摄像头文件：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:property name="camera_length" value="0.02" /> 
    <xacro:property name="camera_width" value="0.05" /> 
    <xacro:property name="camera_height" value="0.05" /> 
    <xacro:property name="joint_camera_x" value="0.08" /> 
    <xacro:property name="joint_camera_y" value="0" />
    <xacro:property name="joint_camera_z" value="${base_length / 2 + camera_height / 2}" />



    <link name="camera">
        <visual>
            <geometry>
                <box size="${camera_length} ${camera_width} ${camera_height}" />
            </geometry>
            <material name="black">
                <color rgba="0 0 0 0.8" />
            </material>
        </visual>
    </link>

    <joint name="camera2base" type="fixed">
        <parent link="base_link" />
        <child link="camera" />
        <origin xyz="${joint_camera_x} ${joint_camera_y} ${joint_camera_z}" ryp="0 0 0" />
    </joint> 

</robot>
```



4.编写雷达文件：

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">

    <xacro:property name="support_radius" value="0.01" />
    <xacro:property name="support_length" value="0.15" />
    <xacro:property name="laser_radius" value="0.03" />
    <xacro:property name="laser_length" value="0.05" />

    <xacro:property name="joint_support_x" value="0" />
    <xacro:property name="joint_support_y" value="0" />
    
    <xacro:property name="joint_support_z" value="${base_length / 2 + support_length / 2}" />

    <xacro:property name="joint_laser_x" value="0" />
    <xacro:property name="joint_laser_y" value="0" />
   
    <xacro:property name="joint_laser_z" value="${support_length / 2 + laser_length / 2}" />

   
    <link name="support">
        <visual>
            <geometry>
                <cylinder radius="${support_radius}" length="${support_length}" />
            </geometry>
            <material name="yellow">
                <color rgba="0.8 0.5 0.0 0.5" />
            </material>
        </visual>
    </link>
    <joint name="support2base" type="fixed">
        <parent link="base_link" />
        <child link="support" />
        <origin xyz="${joint_support_x} ${joint_support_y} ${joint_support_z}" rpq="0 0 0" />
        
    </joint>

    <link name="laser">
        <visual>
            <geometry>
                <cylinder radius="${laser_radius}" length="${laser_length}" />
            </geometry>
            <material name="black">
                <color rgba="0 0 0 0.5" />
            </material>
        </visual>
    </link>
    <joint name="laser2support" type="fixed">
        <parent link="support" />
        <child link="laser" />
        <origin xyz="${joint_laser_x} ${joint_laser_y} ${joint_laser_z}" rpq="0 0 0" />
        
    </joint>
    
</robot>
```



注意：1.文件中不要包含中文

​			2.整合文件中包含所用文件名目录即可，若不在同一目录，需要显示出是哪个文件夹



### 6.4 URDF集成Gazebo

#### 6.4.1 URDF与Gazebo基本集成流程

URDF 与 Gazebo 集成流程与 Rviz 实现类似，主要步骤如下:

1. 创建功能包，导入依赖项
2. 编写 URDF 或 Xacro 文件
3. 启动 Gazebo 并显示机器人模型

**1.创建功能包**

创建新功能包，导入依赖包: urdf、xacro、gazebo_ros、gazebo_ros_control、gazebo_plugins

**2.编写URDF文件**

```xml
<robot name="mycar">
    <link name="base_link">
        <visual>
            <geometry>
                <box size="0.5 0.3 0.1" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="yellow">
                <color rgba="0.5 0.3 0 1" />
            </material>
        </visual>

        <collision>
            <geometry>
                <box size="0.5 0.3 0.1" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
        </collision>

        <inertial>
            <origin xyz="0 0 0" />
            <mass value="2" />
            <inertia ixx="1" ixy="0" ixz="0" iyy="0" iyz="1" izz="1" />
        </inertial>

    </link>
    
    <gazebo reference="base_link">
        <material>Gazebo/Black</material>
    </gazebo>

</robot>
```

注意， 当 URDF 需要与 Gazebo 集成时，和 Rviz 有明显区别:

1.==必须使用 collision 标签==，因为既然是仿真环境，那么必然涉及到碰撞检测，collision 提供碰撞检测的依据，==一般直接复制visual除颜色内容==。

2.==必须使用 inertial 标签==，此标签标注了当前机器人某个刚体部分的惯性矩阵，用于一些力学相关的仿真计算，==一般直接调用宏函数。==

3.颜色设置，也需要==重新使用 gazebo 标签标注颜色==，因为之前的颜色设置为了方便调试包含透明度，仿真环境下没有此选项

**3.launch文件的编写**

```xml
<launch>

    <param name="robot_description" textfile="$(find urdf02_gazebo)/urdf/demo01_helloworld.urdf" />
    <include file="$(find gazebo_ros)/launch/empty_world.launch" />
    <node pkg="gazebo_ros" type="spawn_model" name="spawn_model" args="-urdf -model mycar -param robot_description"  />
</launch>
```

注意：1.这里启用的是urdf文件，如果是xacro文件需要在textfile这里修改一下。

​			2.第二行include的意思是启动一个空世界文件。



#### 6.4.2 URDF集成Gazebo相关设置

较之于 rviz，gazebo在集成 URDF 时，需要做些许修改，比如:必须添加 collision 碰撞属性相关参数、必须添加 inertial 惯性矩阵相关参数，另外，如果直接移植 Rviz 中机器人的颜色设置是没有显示的，颜色设置也必须做相应的变更。

**1.collision**

如果机器人link是标准的几何体形状，和link的 visual 属性设置一致即可。

**2.inertial**

惯性矩阵的设置需要结合link的质量与外形参数动态生成，标准的球体、圆柱与立方体的惯性矩阵公式如下(已经封装为 xacro 实现):

球体惯性矩阵

```xml
<!-- Macro for inertia matrix -->
    <xacro:macro name="sphere_inertial_matrix" params="m r">
        <inertial>
            <mass value="${m}" />
            <inertia ixx="${2*m*r*r/5}" ixy="0" ixz="0"
                iyy="${2*m*r*r/5}" iyz="0" 
                izz="${2*m*r*r/5}" />
        </inertial>
    </xacro:macro>
Copy
```

圆柱惯性矩阵

```xml
<xacro:macro name="cylinder_inertial_matrix" params="m r h">
        <inertial>
            <mass value="${m}" />
            <inertia ixx="${m*(3*r*r+h*h)/12}" ixy = "0" ixz = "0"
                iyy="${m*(3*r*r+h*h)/12}" iyz = "0"
                izz="${m*r*r/2}" /> 
        </inertial>
    </xacro:macro>
Copy
```

立方体惯性矩阵

```xml
 <xacro:macro name="Box_inertial_matrix" params="m l w h">
       <inertial>
               <mass value="${m}" />
               <inertia ixx="${m*(h*h + l*l)/12}" ixy = "0" ixz = "0"
                   iyy="${m*(w*w + l*l)/12}" iyz= "0"
                   izz="${m*(w*w + h*h)/12}" />
       </inertial>
   </xacro:macro>
Copy
```

需要注意的是，原则上，除了 base_footprint 外，机器人的每个刚体部分都需要设置惯性矩阵，且惯性矩阵必须经计算得出，如果随意定义刚体部分的惯性矩阵，那么可能会导致机器人在 Gazebo 中出现抖动，移动等现象。

**3.颜色设置**

在 gazebo 中显示 link 的颜色，必须要使用指定的标签:

```xml
<gazebo reference="link节点名称">
     <material>Gazebo/Blue</material>
</gazebo>
Copy
```

**PS：**material 标签中，设置的值区分大小写，颜色可以设置为 Red Blue Green Black .....

**4.问题汇总：**

在运行gazebo时，经常出现“[gazebo-2] process has died [pid 7920, exit code 255, cmd /opt/ros/melodic/lib/gazebo_ros/gzserver”，导致gazebo界面黑屏或出现一个空图

解决办法：使用Ctrl+C结束当前运行，然后输入

```xml
killall gzserver
```



再次roslaunch，问题解决。

示例：

```xml
<link name="base_link">
        <visual>
            <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="yellow">
                <color rgba="0.8 0.3 0.1 0.5" />
            </material>
            <collision>
                <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            </collision>
            <xacro:cylinder_inertial_matrix m="${base_mass}" r="${base_radius}" h="${base_length}" />
        </visual>
    </link>
```



#### 6.4.3 URDF集成Gazebo实操

**需求描述:**

将之前的机器人模型(xacro版)显示在 gazebo 中

**结果演示:**![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/18_gazebo%E6%A1%88%E4%BE%8B.png)**实现流程:**

1. 需要编写封装惯性矩阵算法的 xacro 文件
2. 为机器人模型中的每一个 link 添加 collision 和 inertial 标签，并且重置颜色属性
3. 在 launch 文件中启动 gazebo 并添加机器人模型



**1.封装惯性矩阵算法的Xacro文件：**

```xml
<robot name="base" xmlns:xacro="http://wiki.ros.org/xacro">
    <!-- Macro for inertia matrix -->
    <xacro:macro name="sphere_inertial_matrix" params="m r">
        <inertial>
            <mass value="${m}" />
            <inertia ixx="${2*m*r*r/5}" ixy="0" ixz="0"
                iyy="${2*m*r*r/5}" iyz="0" 
                izz="${2*m*r*r/5}" />
        </inertial>
    </xacro:macro>

    <xacro:macro name="cylinder_inertial_matrix" params="m r h">
        <inertial>
            <mass value="${m}" />
            <inertia ixx="${m*(3*r*r+h*h)/12}" ixy = "0" ixz = "0"
                iyy="${m*(3*r*r+h*h)/12}" iyz = "0"
                izz="${m*r*r/2}" /> 
        </inertial>
    </xacro:macro>

    <xacro:macro name="Box_inertial_matrix" params="m l w h">
       <inertial>
               <mass value="${m}" />
               <inertia ixx="${m*(h*h + l*l)/12}" ixy = "0" ixz = "0"
                   iyy="${m*(w*w + l*l)/12}" iyz= "0"
                   izz="${m*(w*w + h*h)/12}" />
       </inertial>
   </xacro:macro>
</robot>

```

这个文件以后复制粘贴即可，是惯性矩阵宏

**2.汇总文件：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="head.xacro" />
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

</robot>
```



**3.launch文件：**

```xml
<launch>

    <param name="robot_description" command="$(find xacro)/xacro $(find urdf02_gazebo)/urdf/car.urdf.xacro" />
    <include file="$(find gazebo_ros)/launch/empty_world.launch" />
    <node pkg="gazebo_ros" type="spawn_model" name="spawn_model" args="-urdf -model mycar -param robot_description"  />
</launch>
```



**4.底盘文件：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">

    <xacro:property name="footprint_radius" value="0.001" />

    <link name="base_footprint">
        <visual>
            <geometry>
                <sphere radius="${footprint_radius}" />
            </geometry>
        </visual>
    </link>

    <xacro:property name="base_radius" value="0.1" />
    <xacro:property name="base_length" value="0.08" />
    <xacro:property name="base_mass" value="2" />
    <xacro:property name="lidi" value="0.015" />
    <xacro:property name="base_joint_z" value="${base_length / 2 + lidi}" />

    <link name="base_link">
        <visual>
            <geometry>
                <cylinder radius="0.1" length="0.08" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="yellow">
                <color rgba="0.8 0.3 0.1 0.5" />
            </material>
        </visual>

            <collision>
                <geometry>
                    <cylinder radius="0.1" length="0.08" />
                </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            </collision>

            <xacro:cylinder_inertial_matrix m="${base_mass}" r="${base_radius}" h="${base_length}" />

    </link>

    <gazebo reference="base_link">
        <material>Gazebo/Yellow</material>
    </gazebo>

    <joint name="base_link2base_footprint" type="fixed">
        <parent link="base_footprint" />
        <child link="base_link"/>
        <origin xyz="0 0 0.055" />
    </joint>


    <xacro:property name="wheel_radius" value="0.0325" />
    <xacro:property name="wheel_length" value="0.015" />
    <xacro:property name="wheel_mass" value="0.05" />
    <xacro:property name="PI" value="3.1415927" />

    <xacro:property name="wheel_joint_z" value="${(base_length/2 + lidi - wheel_radius) * -1}" />

    <xacro:macro name="wheel_func" params="wheel_name flag">
    <link name="${wheel_name}_wheel">
        <visual>
            <geometry>
                <cylinder radius="${wheel_radius}" length="${wheel_length}" />
            </geometry>
            <origin xyz="0 0 0" rpy="${PI / 2} 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>
    
    <collision>
        <geometry>
                <cylinder radius="${wheel_radius}" length="${wheel_length}" />
            </geometry>
            <origin xyz="0 0 0" rpy="${PI / 2} 0 0" />
    </collision>

    <xacro:cylinder_inertial_matrix m="${wheel_mass}" r="${wheel_radius}" h="${wheel_length}" />

    </link>

    <gazebo reference="${wheel_name}_wheel">
        <material>Gazebo/Red</material>
    </gazebo>

    <joint name="${wheel_name}2base_link" type="continuous">
        <parent link="base_link" />
        <child link="${wheel_name}_wheel" />
        <origin xyz="0 ${0.1 * flag} ${wheel_joint_z}" rpy="0 0 0"/>
        <axis xyz="0 1 0" />
    </joint>
    </xacro:macro>

    <xacro:wheel_func wheel_name="left" flag="1" />
    <xacro:wheel_func wheel_name="right" flag="-1" />


    <xacro:property name="small_wheel_radius" value="0.0075" />
    <xacro:property name="small_wheel_mass" value="0.03" />
    <xacro:property name="small_joint_z" value="${(base_length / 2 + lidi -small_wheel_radius) * -1}" />

    <xacro:macro name="small_wheel_func" params="small_wheel_name flag">
    <link name="${small_wheel_name}_wheel">
        <visual>
            <geometry>
                <sphere radius="${small_wheel_radius}" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
            <material name="black">
                <color rgba="0.0 0.0 0.0 1.0" />
            </material>
        </visual>

        <collision>
            <geometry>
                <sphere radius="${small_wheel_radius}" />
            </geometry>
            <origin xyz="0 0 0" rpy="0 0 0" />
        </collision>

        <xacro:sphere_inertial_matrix m="${small_wheel_mass}" r="${small_wheel_radius}" />

    </link>

    <gazebo reference="${small_wheel_name}_wheel">
        <material>Gazebo/Red</material>
    </gazebo>

    <joint name="${small_wheel_name}2base_link" type="continuous">
        <parent link="base_link" />
        <child link="${small_wheel_name}_wheel" />
        <origin xyz="${0.08 * flag} 0 ${small_joint_z}" />
        <axis xyz="1 1 1" />
    </joint>
    </xacro:macro>

    <xacro:small_wheel_func small_wheel_name="front" flag="1" />
    <xacro:small_wheel_func small_wheel_name="back" flag="-1" />
</robot>
```



**5.摄像头文件：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:property name="camera_length" value="0.02" /> 
    <xacro:property name="camera_width" value="0.05" /> 
    <xacro:property name="camera_height" value="0.05" /> 
    <xacro:property name="camera_mass" value="0.01" /> 

    <xacro:property name="joint_camera_x" value="0.08" /> 
    <xacro:property name="joint_camera_y" value="0" />
    <xacro:property name="joint_camera_z" value="${base_length / 2 + camera_height / 2}" />



    <link name="camera">
        <visual>
            <geometry>
                <box size="${camera_length} ${camera_width} ${camera_height}" />
            </geometry>
            <material name="black">
                <color rgba="0 0 0 0.8" />
            </material>
        </visual>

        <collision>
            <geometry>
                <box size="${camera_length} ${camera_width} ${camera_height}" />
            </geometry>
        </collision>

        <xacro:Box_inertial_matrix m="${camera_mass}" l="${camera_length}" w="${camera_width}" h="${camera_height}" />
        
    </link>

    <gazebo reference="camera">
        <material>Gazebo/Blue</material>
    </gazebo>

    <joint name="camera2base" type="fixed">
        <parent link="base_link" />
        <child link="camera" />
        <origin xyz="${joint_camera_x} ${joint_camera_y} ${joint_camera_z}" ryp="0 0 0" />
    </joint> 

</robot>
```



**6.雷达文件：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">

    <xacro:property name="support_radius" value="0.01" />
    <xacro:property name="support_length" value="0.15" />
    <xacro:property name="support_mass" value="0.02" />
    <xacro:property name="laser_radius" value="0.03" />
    <xacro:property name="laser_length" value="0.05" />
    <xacro:property name="laser_mass" value="0.1" />

    <xacro:property name="joint_support_x" value="0" />
    <xacro:property name="joint_support_y" value="0" />
    
    <xacro:property name="joint_support_z" value="${base_length / 2 + support_length / 2}" />

    <xacro:property name="joint_laser_x" value="0" />
    <xacro:property name="joint_laser_y" value="0" />
   
    <xacro:property name="joint_laser_z" value="${support_length / 2 + laser_length / 2}" />

   
    <link name="support">
        <visual>
            <geometry>
                <cylinder radius="${support_radius}" length="${support_length}" />
            </geometry>
            <material name="yellow">
                <color rgba="0.8 0.5 0.0 0.5" />
            </material>
        </visual>

        <collision>
            <geometry>
                <cylinder radius="${support_radius}" length="${support_length}" />
            </geometry>
        </collision>

        <xacro:cylinder_inertial_matrix m="${support_mass}" r="${support_radius}" h="${support_length}" />

    </link>

    <gazebo reference="support">
        <material>Gazebo/White</material>
    </gazebo>

    <joint name="support2base" type="fixed">
        <parent link="base_link" />
        <child link="support" />
        <origin xyz="${joint_support_x} ${joint_support_y} ${joint_support_z}" rpq="0 0 0" />
        
    </joint>

    <link name="laser">
        <visual>
            <geometry>
                <cylinder radius="${laser_radius}" length="${laser_length}" />
            </geometry>
            <material name="black">
                <color rgba="0 0 0 0.5" />
            </material>
        </visual>

        <collision>
            <geometry>
                <cylinder radius="${laser_radius}" length="${laser_length}" />
            </geometry>
        </collision>

        <xacro:cylinder_inertial_matrix m="${laser_mass}" r="${laser_radius}" h="${laser_length}" />

    </link>

    <gazebo reference="laser">
        <material>Gazebo/White</material>
    </gazebo>

    <joint name="laser2support" type="fixed">
        <parent link="support" />
        <child link="laser" />
        <origin xyz="${joint_laser_x} ${joint_laser_y} ${joint_laser_z}" rpq="0 0 0" />
        
    </joint>
    
</robot>
```



注意：1.当运行玩gazebo后，记得使用ctrl+c或ctrl+z来结束进程

​			2.当运行gazebo时报错，终端输入`killall gzserver`来杀死gazebo

​			3.collision碰撞属性是在==link内，visual外==

​			4.interial惯性矩阵最好直接调用宏文件，位置同collision

​			5.使用gazebo语句定义颜色时，位置是在link和joint外面。



#### 6.4.4 Gazebo仿真环境搭建

**1.将预先下载好的文件复制到worlds文件夹下：**

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230227192653.png)



**2.编写launch文件：**

```xml
<launch>

    <param name="robot_description" command="$(find xacro)/xacro $(find urdf02_gazebo)/urdf/car.urdf.xacro" />
    <include file="$(find gazebo_ros)/launch/empty_world.launch">
        <arg name="world_name" value="$(find urdf02_gazebo)/worlds/box_house.world" />
    </include>
    <node pkg="gazebo_ros" type="spawn_model" name="spawn_model" args="-urdf -model mycar -param robot_description"  />
</launch>
```



注意：1.==第一个include下没有/==

​			2.gazebo文件想正常运行，要将3D渲染关掉

### 6.5 URDF.Gazebo与Rviz综合运用

#### 6.5.1 机器人运动控制以及里程计信息显示



**1.运动控制实现流程(Gazebo)**：

新建运动控制文件：

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230227200511.png)

代码示例：

```xml
<robot name="my_car_move" xmlns:xacro="http://wiki.ros.org/xacro">

   
    <xacro:macro name="joint_trans" params="joint_name">
        
        <transmission name="${joint_name}_trans">
            <type>transmission_interface/SimpleTransmission</type>
            <joint name="${joint_name}">
                <hardwareInterface>hardware_interface/VelocityJointInterface</hardwareInterface>
            </joint>
            <actuator name="${joint_name}_motor">
                <hardwareInterface>hardware_interface/VelocityJointInterface</hardwareInterface>
                <mechanicalReduction>1</mechanicalReduction>
            </actuator>
        </transmission>
    </xacro:macro>

    
    <xacro:joint_trans joint_name="left2base_link" />
    <xacro:joint_trans joint_name="right2base_link" />

    
    <gazebo>
        <plugin name="differential_drive_controller" filename="libgazebo_ros_diff_drive.so">
            <rosDebugLevel>Debug</rosDebugLevel>
            <publishWheelTF>true</publishWheelTF>
            <robotNamespace>/</robotNamespace>
            <publishTf>1</publishTf>
            <publishWheelJointState>true</publishWheelJointState>
            <alwaysOn>true</alwaysOn>
            <updateRate>100.0</updateRate>
            <legacyMode>true</legacyMode>
            <leftJoint>left2base_link</leftJoint> 	<!--左轮关节名-->
            <rightJoint>right2base_link</rightJoint> 	<!--右轮关节名-->
            <wheelSeparation>${base_radius * 2}</wheelSeparation>	<!--两轮间距--> 
            <wheelDiameter>${wheel_radius * 2}</wheelDiameter> 		<!--车轮直径-->
            <broadcastTF>1</broadcastTF>
            <wheelTorque>30</wheelTorque>
            <wheelAcceleration>1.8</wheelAcceleration>
            <commandTopic>cmd_vel</commandTopic> 	<!-- 运动控制话题 -->
            <odometryFrame>odom</odometryFrame> 
            <odometryTopic>odom</odometryTopic>		<!--里程计话题-->
            <robotBaseFrame>base_footprint</robotBaseFrame> 	<!--极坐标系-->
        </plugin>
    </gazebo>

</robot>
```





**2.将代码集成之文件内，并启用launch文件**：



```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="head.xacro" />
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

    <xacro:include filename="gazebo/move.xacro" />
    
</robot>
```

注意：集成move.xacro文件时，要加上前缀gazebo/，这样才能向系统显示是哪个文件要被调用



```xml
<launch>

    <param name="robot_description" command="$(find xacro)/xacro $(find urdf02_gazebo)/urdf/car.urdf.xacro" />
    <include file="$(find gazebo_ros)/launch/empty_world.launch">
        <arg name="world_name" value="$(find urdf02_gazebo)/worlds/box_house.world" />
    </include>
    <node pkg="gazebo_ros" type="spawn_model" name="spawn_model" args="-urdf -model mycar -param robot_description"  />
</launch>
```

注意：1.include下包含的世界文件，要率先复制到文件夹worlds下。

​			2.在启动Gazebo后，如果想控制小车运动，在终端输入以下语句：

```xml
rosrun teleop_twist_keyboard teleop_twist_keyboard.py _speed:=0.3 _turn:=0.5
```



**3.Rviz查看里程计信息**

编写launch文件启动rviz：

```xml
<launch>
   
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find urdf01_rviz)/config/show_mycar.rviz" />
    <node pkg="joint_state_publisher" type="joint_state_publisher" name="joint_state_publisher" output="screen" />
    <node pkg="robot_state_publisher" type="robot_state_publisher" name="robot_state_publisher" output="screen" />

</launch>
```

执行 launch 文件后，在 Rviz 中添加图示组件:![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/21_Rviz%E6%98%BE%E7%A4%BA%E9%87%8C%E7%A8%8B%E8%AE%A1%E6%95%B0%E6%8D%AE.png)





#### 6.5.2 雷达信息仿真以及显示



**1.Gazebo仿真雷达**：

```xml
<robot name="my_sensors" xmlns:xacro="http://wiki.ros.org/xacro">

  <!-- 雷达 -->
  <gazebo reference="laser">			<!--雷达在link中的名称-->
    <sensor type="ray" name="rplidar">	<!--type是雷达类型，name是雷达名字-->
      <pose>0 0 0 0 0 0</pose>			<!--偏移量，和俯仰角-->	
      <visualize>true</visualize>		<!--雷达射线是否可视化，true则可以看见，false则不能看见-->
      <update_rate>5.5</update_rate>	<!--雷达射线更新频率，1s钟更新5.5次-->
      <ray>
        <scan>
          <horizontal>
            <samples>360</samples>		<!--雷达旋转一周会发射多少个射线-->
            <resolution>1</resolution>	<!--分辨率，1代表每个射线都测距，2代表每两个射线里测距一次-->
            <min_angle>-3</min_angle>	<!--采样角度中轴向左实现角度，弧度制-->
            <max_angle>3</max_angle>	<!--采样角度中轴向右实现角度，弧度制-->
          </horizontal>
        </scan>
        <range>
          <min>0.10</min>				<!--雷达采样有效距离最小值-->
          <max>30.0</max>				<!--雷达采样有效距离最大值-->
          <resolution>0.01</resolution>	<!--采样精度-->
        </range>
        <noise>
          <type>gaussian</type>			<!--雷达的采样误差-->
          <mean>0.0</mean>
          <stddev>0.01</stddev>
        </noise>
      </ray>
      <plugin name="gazebo_rplidar" filename="libgazebo_ros_laser.so">
        <topicName>/scan</topicName>
        <frameName>laser</frameName>
      </plugin>
    </sensor>
  </gazebo>

</robot>

```



**2.xacro文件集成：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="head.xacro" />
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

    <xacro:include filename="gazebo/move.xacro" />
    <xacro:include filename="gazebo/laser.xacro" />
    
</robot>
```



**3.启用launch文件**



**4.Rviz雷达数据显示：**

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230228105236.png)

注意：1.Fixed Frame要修改成odom

​			2.添加LaserScan的话题改为/scan

​			3.如果红点过小，size可以改为0.05。



#### 6.5.3 摄像头信息仿真以及显示



**1.摄像头代码示例：**

```xml
<robot name="my_sensors" xmlns:xacro="http://wiki.ros.org/xacro">
  <!-- 被引用的link -->
  <gazebo reference="camera">
    <!-- 类型设置为 camara -->
    <sensor type="camera" name="camera_node">
      <update_rate>30.0</update_rate> <!-- 更新频率 -->
      <!-- 摄像头基本信息设置 -->
      <camera name="head">
        <horizontal_fov>1.3962634</horizontal_fov>
        <image>
          <width>1280</width>
          <height>720</height>
          <format>R8G8B8</format>
        </image>
        <clip>
          <near>0.02</near>
          <far>300</far>
        </clip>
        <noise>
          <type>gaussian</type>
          <mean>0.0</mean>
          <stddev>0.007</stddev>
        </noise>
      </camera>
      <!-- 核心插件 -->
      <plugin name="gazebo_camera" filename="libgazebo_ros_camera.so">
        <alwaysOn>true</alwaysOn>
        <updateRate>0.0</updateRate>
        <cameraName>/camera</cameraName>
        <imageTopicName>image_raw</imageTopicName>
        <cameraInfoTopicName>camera_info</cameraInfoTopicName>
        <frameName>camera</frameName>
        <hackBaseline>0.07</hackBaseline>
        <distortionK1>0.0</distortionK1>
        <distortionK2>0.0</distortionK2>
        <distortionK3>0.0</distortionK3>
        <distortionT1>0.0</distortionT1>
        <distortionT2>0.0</distortionT2>
      </plugin>
    </sensor>
  </gazebo>
</robot>

```



**2.xacro汇总文件的编写：**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="head.xacro" />
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

    <xacro:include filename="gazebo/move.xacro" />
    <xacro:include filename="gazebo/laser.xacro" />
    <xacro:include filename="gazebo/camera.xacro" />
    
</robot>
```



**3.启用launch文件**



**4.配置Rviz环境：**

![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230228110952.png)



![QQ图片20230228110922](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230228110922.png)



#### 6.5.4 kinect信息仿真以及显示

通过 Gazebo 模拟kinect摄像头，并在 Rviz 中显示kinect摄像头数据。



**1.搭建kinect文件**：

```xml
robot name="my_sensors" xmlns:xacro="http://wiki.ros.org/xacro">
    <gazebo reference="support">  
      <sensor type="depth" name="camera">
        <always_on>true</always_on>
        <update_rate>20.0</update_rate>
        <camera>
          <horizontal_fov>${60.0*PI/180.0}</horizontal_fov>
          <image>
            <format>R8G8B8</format>
            <width>640</width>
            <height>480</height>
          </image>
          <clip>
            <near>0.05</near>
            <far>8.0</far>
          </clip>
        </camera>
        <plugin name="kinect_camera_controller" filename="libgazebo_ros_openni_kinect.so">
          <cameraName>camera</cameraName>
          <alwaysOn>true</alwaysOn>
          <updateRate>10</updateRate>
          <imageTopicName>rgb/image_raw</imageTopicName>
          <depthImageTopicName>depth/image_raw</depthImageTopicName>
          <pointCloudTopicName>depth/points</pointCloudTopicName>
          <cameraInfoTopicName>rgb/camera_info</cameraInfoTopicName>
          <depthImageCameraInfoTopicName>depth/camera_info</depthImageCameraInfoTopicName>
          <frameName>support_depth</frameName>	<!--如果使用点阵云，就用support_depth，否则使用support即可-->
          <baseline>0.1</baseline>
          <distortion_k1>0.0</distortion_k1>
          <distortion_k2>0.0</distortion_k2>
          <distortion_k3>0.0</distortion_k3>
          <distortion_t1>0.0</distortion_t1>
          <distortion_t2>0.0</distortion_t2>
          <pointCloudCutoff>0.4</pointCloudCutoff>
        </plugin>
      </sensor>
    </gazebo>

</robot>
```



**2.编写汇总文件**

```xml
<robot name="mycar" xmlns:xacro="http://wiki.ros.org/xacro">
    <xacro:include filename="head.xacro" />
    <xacro:include filename="demo05_car_base.urdf.xacro" />
    <xacro:include filename="demo06_car_camera.urdf.xacro" />
    <xacro:include filename="demo07_car_laser.urdf.xacro" />

    <xacro:include filename="gazebo/move.xacro" />
    <xacro:include filename="gazebo/laser.xacro" />
    <xacro:include filename="gazebo/camera.xacro" />
    <xacro:include filename="gazebo/kinect.xacro" />

</robot>
```

**3.编写launch文件：**

在启动rviz文件中添加语句：

```xml
<node pkg="tf2_ros" type="static_transform_publisher" name="static_transform_publisher" args="0 0 0 -1.57 0 -1.57 /support /support_depth" />
```

**4.配置Rviz环境：**

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E7%82%B9%E4%BA%91%E6%95%B0%E6%8D%AE_%E4%BF%AE%E6%AD%A3.png)





## 7.机器人导航(仿真)

### 7.1 概述

#### 7.1.1导航模块简介

机器人是如何实现导航的呢？或换言之，机器人是如何从 A 点移动到 B 点呢？ROS 官方为了提供了一张导航功能包集的图示,该图中囊括了 ROS 导航的一些关键技术:![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/02_%E5%AF%BC%E8%88%AA%E5%AE%98%E6%96%B9%E6%9E%B6%E6%9E%84.png)

假定我们已经以特定方式配置机器人，导航功能包集将使其可以运动。上图概述了这种配置方式。白色的部分是必须且已实现的组件，灰色的部分是可选且已实现的组件，蓝色的部分是必须为每一个机器人平台创建的组件。

总结下来，涉及的关键技术有如下五点:

1. 全局地图
2. 自身定位
3. 路径规划
4. 运动控制
5. 环境感知

机器人导航实现与无人驾驶类似，关键技术也是由上述五点组成，只是无人驾驶是基于室外的，而我们当前介绍的机器人导航更多是基于室内的。

**1.全局地图**

在现实生活中，当我们需要实现导航时，可能会首先参考一张全局性质的地图，然后根据地图来确定自身的位置、目的地位置，并且也会根据地图显示来规划一条大致的路线.... 对于机器人导航而言，也是如此，在机器人导航中地图是一个重要的组成元素，当然如果要使用地图，首先需要绘制地图。关于地图建模技术不断涌现，这其中有一门称之为 SLAM 的理论脱颖而出:

1. **SLAM**(simultaneous localization and mapping),也称为CML (Concurrent Mapping and Localization), 即时定位与地图构建，或并发建图与定位。SLAM问题可以描述为: 机器人在未知环境中从一个未知位置开始移动,在移动过程中根据位置估计和地图进行自身定位，同时在自身定位的基础上建造增量式地图，以绘制出外部环境的完全地图。
2. 在 ROS 中，较为常用的 SLAM 实现也比较多，比如: gmapping、hector_slam、cartographer、rgbdslam、ORB_SLAM ....
3. 当然如果要完成 SLAM ，机器人必须要具备感知外界环境的能力，尤其是要具备获取周围环境深度信息的能力。感知的实现需要依赖于传感器，比如: 激光雷达、摄像头、RGB-D摄像头...
4. SLAM 可以用于地图生成，而生成的地图还需要被保存以待后续使用，在 ROS 中保存地图的功能包是 map_server

另外注意: SLAM 虽然是机器人导航的重要技术之一，但是 二者并不等价，确切的讲，SLAM 只是实现地图构建和即时定位。

**2.自身定位**

导航伊始和导航过程中，机器人都需要确定当前自身的位置，如果在室外，那么 GPS 是一个不错的选择，而如果室内、隧道、地下或一些特殊的屏蔽 GPS 信号的区域，由于 GPS 信号弱化甚至完全不可用，那么就必须另辟蹊径了，比如前面的 SLAM 就可以实现自身定位，除此之外，ROS 中还提供了一个用于定位的功能包: amcl

**amcl**(adaptiveMonteCarloLocalization)自适应的蒙特卡洛定位,是用于2D移动机器人的概率定位系统。它实现了自适应（或KLD采样）蒙特卡洛定位方法，该方法使用粒子过滤器根据已知地图跟踪机器人的姿态。

**3.路径规划**

导航就是机器人从A点运动至B点的过程，在这一过程中，机器人需要根据目标位置计算全局运动路线，并且在运动过程中，还需要时时根据出现的一些动态障碍物调整运动路线，直至到达目标点，该过程就称之为路径规划。在 ROS 中提供了 move_base 包来实现路径规则,该功能包主要由两大规划器组成:

1. 全局路径规划(gloable_planner)

   根据给定的目标点和全局地图实现总体的路径规划，使用 Dijkstra 或 A* 算法进行全局路径规划，计算最优路线，作为全局路线

2. 本地时时规划(local_planner)

   在实际导航过程中，机器人可能无法按照给定的全局最优路线运行，比如:机器人在运行中，可能会随时出现一定的障碍物... 本地规划的作用就是使用一定算法(Dynamic Window Approaches) 来实现障碍物的规避，并选取当前最优路径以尽量符合全局最优路径

全局路径规划与本地路径规划是相对的，全局路径规划侧重于全局、宏观实现，而本地路径规划侧重与当前、微观实现。

**4.运动控制**

导航功能包集假定它可以通过话题"cmd_vel"发布`geometry_msgs/Twist`类型的消息，这个消息基于机器人的基座坐标系，它传递的是运动命令。这意味着必须有一个节点订阅"cmd_vel"话题， 将该话题上的速度命令转换为电机命令并发送。

**5.环境感知**

感知周围环境信息，比如: 摄像头、激光雷达、编码器...，摄像头、激光雷达可以用于感知外界环境的深度信息，编码器可以感知电机的转速信息，进而可以获取速度信息并生成里程计信息。

在导航功能包集中，环境感知也是一重要模块实现，它为其他模块提供了支持。其他模块诸如: SLAM、amcl、move_base 都需要依赖于环境感知。





#### 7.1.2 导航之坐标系

**1.简介**

定位是导航中的重要实现之一，所谓定位，就是参考某个坐标系(比如:以机器人的出发点为原点创建坐标系)在该坐标系中标注机器人。定位原理看似简单，但是这个这个坐标系不是客观存在的，我们也无法以上帝视角确定机器人的位姿，定位实现需要依赖于机器人自身，机器人需要逆向推导参考系原点并计算坐标系相对关系，该过程实现常用方式有两种:

- 通过里程计定位:时时收集机器人的速度信息计算并发布机器人坐标系与父级参考系的相对关系。
- 通过传感器定位:通过传感器收集外界环境信息通过匹配计算并发布机器人坐标系与父级参考系的相对关系。

两种方式在导航中都会经常使用。

**2.特点**

两种定位方式都有各自的优缺点。

里程计定位:

- 优点:里程计定位信息是连续的，没有离散的跳跃。
- 缺点:里程计存在累计误差，不利于长距离或长期定位。

传感器定位:

- 优点:比里程计定位更精准；
- 缺点:传感器定位会出现跳变的情况，且传感器定位在标志物较少的环境下，其定位精度会大打折扣。

两种定位方式优缺点互补，应用时一般二者结合使用。

**3.坐标系变换**

上述两种定位实现中，机器人坐标系一般使用机器人模型中的根坐标系(base_link 或 base_footprint)，里程计定位时，父级坐标系一般称之为 odom，如果通过传感器定位，父级参考系一般称之为 map。当二者结合使用时，map 和 odom 都是机器人模型根坐标系的父级，这是不符合坐标变换中"单继承"的原则的，所以，一般会将转换关系设置为: map -> doom -> base_link 或 base_footprint。



![](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/QQ%E5%9B%BE%E7%89%8720230228140130.jpg)





### 7.2 导航实现



#### 7.2.1 导航实现01_SLAM建图



**1.gmapping简介**

gmapping 是ROS开源社区中较为常用且比较成熟的SLAM算法之一，gmapping可以根据移动机器人里程计数据和激光雷达数据来绘制二维的栅格地图，对应的，gmapping对硬件也有一定的要求:

- 该移动机器人可以发布里程计消息
- 机器人需要发布雷达消息(该消息可以通过水平固定安装的雷达发布，或者也可以将深度相机消息转换成雷达消息)

关于里程计与雷达数据，仿真环境中可以正常获取的，不再赘述，栅格地图如案例所示。

gmapping 安装前面也有介绍，命令如下:

> ```
> sudo apt install ros-<ROS版本>-gmapping
> ```



**2.gmapping节点说明**

gmapping 功能包中的核心节点是:slam_gmapping。为了方便调用，需要先了解该节点订阅的话题、发布的话题、服务以及相关参数。

**2.1订阅的Topic**

tf (tf/tfMessage)

- 用于雷达、底盘与里程计之间的坐标变换消息。

scan(sensor_msgs/LaserScan)

- SLAM所需的雷达信息。

**2.2发布的Topic**

map_metadata(nav_msgs/MapMetaData)

- 地图元数据，包括地图的宽度、高度、分辨率等，该消息会固定更新。

map(nav_msgs/OccupancyGrid)

- 地图栅格数据，一般会在rviz中以图形化的方式显示。

~entropy(std_msgs/Float64)

- 机器人姿态分布熵估计(值越大，不确定性越大)。

**2.3服务**

dynamic_map(nav_msgs/GetMap)

- 用于获取地图数据。

**2.4参数**

~base_frame(string, default:"base_link")

- 机器人基坐标系。

~map_frame(string, default:"map")

- 地图坐标系。

~odom_frame(string, default:"odom")

- 里程计坐标系。

~map_update_interval(float, default: 5.0)

- 地图更新频率，根据指定的值设计更新间隔。

~maxUrange(float, default: 80.0)

- 激光探测的最大可用范围(超出此阈值，被截断)。

~maxRange(float)

- 激光探测的最大范围。

.... 参数较多，上述是几个较为常用的参数，其他参数介绍可参考官网。

**2.5所需的坐标变换**

雷达坐标系→基坐标系

- 一般由 robot_state_publisher 或 static_transform_publisher 发布。

基坐标系→里程计坐标系

- 一般由里程计节点发布。

**2.6发布的坐标变换**

地图坐标系→里程计坐标系

- 地图到里程计坐标系之间的变换。

![image-20200927095254706](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/5c4eb1ec45bdcca93f5ae03016f89a4d.png)

![image-20200927095435992](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/2aa5c5402a58e5c8cfe0135798a23e64.png)

**3.gmapping使用：**

```xml
<launch>
    <!--仿真环境下，将该参数设置为 true-->
	<param name="use_sim_time" value="true"/>
    <!--gmapping节点-->
    <node pkg="gmapping" type="slam_gmapping" name="slam_gmapping" output="screen">
      <!--设置雷达话题-->
      <remap from="scan" to="scan"/>
        
      <!--关键坐标系-->
      
      <param name="base_frame" value="base_footprint" />
      <param name="map_frame" value="map" />
      <param name="odom_frame" value="odom" />
      
      <param name="base_frame" value="base_footprint"/><!--底盘坐标系-->
      <param name="odom_frame" value="odom"/> <!--里程计坐标系-->
      <param name="map_update_interval" value="5.0"/>
      <param name="maxUrange" value="16.0"/>
      <param name="sigma" value="0.05"/>
      <param name="kernelSize" value="1"/>
      <param name="lstep" value="0.05"/>
      <param name="astep" value="0.05"/>
      <param name="iterations" value="5"/>
      <param name="lsigma" value="0.075"/>
      <param name="ogain" value="3.0"/>
      <param name="lskip" value="0"/>
      <param name="srr" value="0.1"/>
      <param name="srt" value="0.2"/>
      <param name="str" value="0.1"/>
      <param name="stt" value="0.2"/>
      <param name="linearUpdate" value="1.0"/>
      <param name="angularUpdate" value="0.5"/>
      <param name="temporalUpdate" value="3.0"/>
      <param name="resampleThreshold" value="0.5"/>
      <param name="particles" value="30"/>
      <param name="xmin" value="-50.0"/>
      <param name="ymin" value="-50.0"/>
      <param name="xmax" value="50.0"/>
      <param name="ymax" value="50.0"/>
      <param name="delta" value="0.05"/>
      <param name="llsamplerange" value="0.01"/>
      <param name="llsamplestep" value="0.01"/>
      <param name="lasamplerange" value="0.005"/>
      <param name="lasamplestep" value="0.005"/>
    </node>

    <node pkg="joint_state_publisher" name="joint_state_publisher" type="joint_state_publisher" />
    <node pkg="robot_state_publisher" name="robot_state_publisher" type="robot_state_publisher" />

    <node pkg="rviz" type="rviz" name="rviz" />
    <!-- 可以保存 rviz 配置并后期直接使用-->
    <!--
    <node pkg="rviz" type="rviz" name="rviz" args="-d $(find my_nav_sum)/rviz/gmapping.rviz"/>
    -->
</launch>

```

关键代码解释：

```xml
<remap from="scan" to="scan"/><!-- 雷达话题 -->
<param name="base_frame" value="base_footprint"/><!--底盘坐标系-->
<param name="odom_frame" value="odom"/> <!--里程计坐标系-->
```



**4.执行：**

1）启动Gazebo节点：

roslaunch urdf02_gazebo demo03_env.launch

2）启动上述地图配置节点：

roslaunch nav_demo nav01_slam.launch

3）启动键盘控制节点，控制机器人运动建模：

rosrun teleop_twist_keyboard teleop_twist_keyboard.py

4）在rviz中添加组件，显示地图

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/slam%E6%BC%94%E7%A4%BA.png)

#### 7.2.2 导航实现02_地图服务

上一节我们已经实现通过gmapping的构建地图并在rviz中显示了地图，不过，上一节中地图数据是保存在内存中的，当节点关闭时，数据也会被一并释放，我们需要将栅格地图序列化到的磁盘以持久化存储，后期还要通过反序列化读取磁盘的地图数据再执行后续操作。在ROS中，地图数据的序列化与反序列化可以通过 map_server 功能包实现。

**1.map_server简介**

map_server功能包中提供了两个节点: map_saver 和 map_server，前者用于将栅格地图保存到磁盘，后者读取磁盘的栅格地图并以服务的方式提供出去。

map_server安装前面也有介绍，命令如下:

> ```
> sudo apt install ros-<ROS版本>-map-server
> ```

**2.map_server使用之地图保存节点(map_saver)**

**2.1map_saver节点说明**

**订阅的topic:**

map(nav_msgs/OccupancyGrid)

- 订阅此话题用于生成地图文件。

**2.2地图保存launch文件**

地图保存的语法比较简单，编写一个launch文件，内容如下:

```xml
<launch>
    <arg name="filename" value="$(find nav_demo)/map/nav" />
    <node name="map_save" pkg="map_server" type="map_saver" args="-f $(arg filename)" />
</launch>
```

其中第一行的map/nav指的是保存文件夹和文件的名字，slam建图完毕后，执行该launch文件即可。

**2.3保存结果解释**

```yaml
#1.声明地图图片资源的路径
image: /home/wangce/demo05_ws/src/nav_demo/map/nav.pgm
#2.地图刻度尺单位是 米/像素
resolution: 0.050000
#3.地图的位姿信息(按照右手坐标系，地图右下角相对于rviz中原点的位姿)
#值1：x方向上的偏移量
#值2：y方向上的偏移量
#值3：地图的偏航角度(单位是弧度)
origin: [-50.000000, -50.000000, 0.000000]

#地图中的障碍物判断：
#最重地图结果：白色是可通行区域，黑色是障碍物，蓝灰是未知区域
#判断规则：
#1.地图中的每个像素都有取值[0,255] 白色：255 黑色：0
#2.根据像素值计算一个比例：p=(255-x)/255，白色是0，黑色是1，灰色是介于0~1的值
#3.判断是否是障碍物，如果p>occupied_thresh就是障碍物，如果p<occupied_thresh就是无物，可以自由通行

#4.占用阈值
occupied_thresh: 0.65
#5.空闲阈值
free_thresh: 0.196
#6.取反，可以颠倒黑白
negate: 0
```





**3.map_server使用之地图服务(map_server)**

**3.1map_server节点说明**

**发布的话题**

map_metadata（nav_msgs / MapMetaData）

- 发布地图元数据。

map（nav_msgs / OccupancyGrid）

- 地图数据。

**服务**

static_map（nav_msgs / GetMap）

- 通过此服务获取地图。

**参数**

〜frame_id（字符串，默认值：“map”）

- 地图坐标系。

**3.2地图读取**

通过 map_server 的 map_server 节点可以读取栅格地图数据，编写 launch 文件如下:

```xml
<launch>
    <!-- 设置地图的配置文件 -->
    <arg name="map" default="nav.yaml" />
    <!-- 运行地图服务器，并且加载设置的地图-->
    <node name="map_server" pkg="map_server" type="map_server" args="$(find nav_demo)/map/$(arg map)"/>
</launch>
Copy
```

其中参数是地图描述文件的资源路径，执行该launch文件，该节点会发布话题:map(nav_msgs/OccupancyGrid)

**3.3地图显示**

在 rviz 中使用 map 组件可以显示栅格地图：

启动rviz，添加map，使话题为map即可看到地图。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E5%9C%B0%E5%9B%BE%E6%98%BE%E7%A4%BA.png)





#### 7.2.3 导航实现03_定位

所谓定位就是推算机器人自身在全局地图中的位置，当然，SLAM中也包含定位算法实现，不过SLAM的定位是用于构建全局地图的，是属于导航开始之前的阶段，而当前定位是用于导航中，导航中，机器人需要按照设定的路线运动，通过定位可以判断机器人的实际轨迹是否符合预期。在ROS的导航功能包集navigation中提供了 amcl 功能包，用于实现导航中的机器人定位。

**1.amcl简介**

AMCL(adaptive Monte Carlo Localization) 是用于2D移动机器人的概率定位系统，它实现了自适应（或KLD采样）蒙特卡洛定位方法，可以根据已有地图使用粒子滤波器推算机器人位置。

amcl已经被集成到了navigation包，navigation安装前面也有介绍，命令如下:

> ```
> sudo apt install ros-<ROS版本>-navigation
> ```

**2.amcl节点说明**

amcl 功能包中的核心节点是:amcl。为了方便调用，需要先了解该节点订阅的话题、发布的话题、服务以及相关参数。

**2.1订阅的Topic**

scan(sensor_msgs/LaserScan)

- 激光雷达数据。

tf(tf/tfMessage)

- 坐标变换消息。

initialpose(geometry_msgs/PoseWithCovarianceStamped)

- 用来初始化粒子滤波器的均值和协方差。

map(nav_msgs/OccupancyGrid)

- 获取地图数据。

**2.2发布的Topic**

amcl_pose(geometry_msgs/PoseWithCovarianceStamped)

- 机器人在地图中的位姿估计。

particlecloud(geometry_msgs/PoseArray)

- 位姿估计集合，rviz中可以被 PoseArray 订阅然后图形化显示机器人的位姿估计集合。

tf(tf/tfMessage)

- 发布从 odom 到 map 的转换。

**2.3服务**

global_localization(std_srvs/Empty)

- 初始化全局定位的服务。

request_nomotion_update(std_srvs/Empty)

- 手动执行更新和发布更新的粒子的服务。

set_map(nav_msgs/SetMap)

- 手动设置新地图和姿态的服务。

**2.4调用的服务**

static_map(nav_msgs/GetMap)

- 调用此服务获取地图数据。

**2.5参数**

~odom_model_type(string, default:"diff")

- 里程计模型选择: "diff","omni","diff-corrected","omni-corrected" (diff 差速、omni 全向轮)

~odom_frame_id(string, default:"odom")

- 里程计坐标系。

~base_frame_id(string, default:"base_link")

- 机器人极坐标系。

~global_frame_id(string, default:"map")

- 地图坐标系。

.... 参数较多，上述是几个较为常用的参数，其他参数介绍可参考官网。

**2.6坐标变换**

里程计本身也是可以协助机器人定位的，不过里程计存在累计误差且一些特殊情况时(车轮打滑)会出现定位错误的情况，amcl 则可以通过估算机器人在地图坐标系下的姿态，再结合里程计提高定位准确度。

- 里程计定位:只是通过里程计数据实现 /odom_frame 与 /base_frame 之间的坐标变换。
- amcl定位: 可以提供 /map_frame 、/odom_frame 与 /base_frame 之间的坐标变换。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/amcl%E5%AE%9A%E4%BD%8D%E5%9D%90%E6%A0%87%E5%8F%98%E6%8D%A2.png)

**3.amcl使用**

**3.1launch文件编写：**

```xml
<launch>
<node pkg="amcl" type="amcl" name="amcl" output="screen">
  <!-- Publish scans from best pose at a max of 10 Hz -->
  <param name="odom_model_type" value="diff"/><!-- 里程计模式为差分 -->
  <param name="odom_alpha5" value="0.1"/>
  <param name="transform_tolerance" value="0.2" />
  <param name="gui_publish_rate" value="10.0"/>
  <param name="laser_max_beams" value="30"/>
  <param name="min_particles" value="500"/>
  <param name="max_particles" value="5000"/>
  <param name="kld_err" value="0.05"/>
  <param name="kld_z" value="0.99"/>
  <param name="odom_alpha1" value="0.2"/>
  <param name="odom_alpha2" value="0.2"/>
  <!-- translation std dev, m -->
  <param name="odom_alpha3" value="0.8"/>
  <param name="odom_alpha4" value="0.2"/>
  <param name="laser_z_hit" value="0.5"/>
  <param name="laser_z_short" value="0.05"/>
  <param name="laser_z_max" value="0.05"/>
  <param name="laser_z_rand" value="0.5"/>
  <param name="laser_sigma_hit" value="0.2"/>
  <param name="laser_lambda_short" value="0.1"/>
  <param name="laser_lambda_short" value="0.1"/>
  <param name="laser_model_type" value="likelihood_field"/>
  <!-- <param name="laser_model_type" value="beam"/> -->
  <param name="laser_likelihood_max_dist" value="2.0"/>
  <param name="update_min_d" value="0.2"/>
  <param name="update_min_a" value="0.5"/>

  <param name="odom_frame_id" value="odom"/><!-- 里程计坐标系 -->
  <param name="base_frame_id" value="base_footprint"/><!-- 添加机器人基坐标系 -->
  <param name="global_frame_id" value="map"/><!-- 添加地图坐标系 -->

  <param name="resample_interval" value="1"/>
  <param name="transform_tolerance" value="0.1"/>
  <param name="recovery_alpha_slow" value="0.0"/>
  <param name="recovery_alpha_fast" value="0.0"/>
</node>
</launch>

```



**3.2编写测试launch文件：**

```xml
<launch>
    <node pkg="joint_state_publisher" name="joint_state_publisher" type="joint_state_publisher" />
    <node pkg="robot_state_publisher" name="robot_state_publisher" type="robot_state_publisher" />
    <node pkg="rviz" type="rviz" name="rviz" />
    <include file="$(find nav_demo)/launch/nav03_map_server.launch" />
    <include file="$(find nav_demo)/launch/nav04_amcl.launch" />
</launch>
```





**3.3执行：**

1.先启动 Gazebo 仿真环境(此过程略)；

2.启动键盘控制节点：

```
rosrun teleop_twist_keyboard teleop_twist_keyboard.py
```

3.启动上一步中集成地图服务、amcl 与 rviz 的 launch 文件；

4.在启动的 rviz 中，添加RobotModel、Map组件，分别显示机器人模型与地图，添加 posearray 插件，设置topic为particlecloud来显示 amcl 预估的当前机器人的位姿，箭头越是密集，说明当前机器人处于此位置的概率越高；

5.通过键盘控制机器人运动，会发现 posearray 也随之而改变。![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/amcl%E6%B5%8B%E8%AF%95.gif)





#### 7.2.4 导航实现04_路径规划

**1.move_base简介**

move_base 功能包提供了基于动作(action)的路径规划实现，move_base 可以根据给定的目标点，控制机器人底盘运动至目标位置，并且在运动过程中会连续反馈机器人自身的姿态与目标点的状态信息。如前所述(7.1)move_base主要由全局路径规划与本地路径规划组成。

**2.move_base节点说明**

move_base功能包中的核心节点是:move_base。为了方便调用，需要先了解该节点action、订阅的话题、发布的话题、服务以及相关参数。

**2.1动作**

**动作订阅**

move_base/goal(move_base_msgs/MoveBaseActionGoal)

- move_base 的运动规划目标。

move_base/cancel(actionlib_msgs/GoalID)

- 取消目标。

**动作发布**

move_base/feedback(move_base_msgs/MoveBaseActionFeedback)

- 连续反馈的信息，包含机器人底盘坐标。

move_base/status(actionlib_msgs/GoalStatusArray)

- 发送到move_base的目标状态信息。

move_base/result(move_base_msgs/MoveBaseActionResult)

- 操作结果(此处为空)。

**2.2订阅的Topic**

move_base_simple/goal(geometry_msgs/PoseStamped)

- 运动规划目标(与action相比，没有连续反馈，无法追踪机器人执行状态)。

**2.3发布的Topic**

cmd_vel(geometry_msgs/Twist)

- 输出到机器人底盘的运动控制消息。

**2.4服务**

~make_plan(nav_msgs/GetPlan)

- 请求该服务，可以获取给定目标的规划路径，但是并不执行该路径规划。

~clear_unknown_space(std_srvs/Empty)

- 允许用户直接清除机器人周围的未知空间。

~clear_costmaps(std_srvs/Empty)

- 允许清除代价地图中的障碍物，可能会导致机器人与障碍物碰撞，请慎用。

**2.5参数**

请参考官网。

**3.move_base与代价地图**

**3.1概念**

机器人导航(尤其是路径规划模块)是依赖于地图的，地图在SLAM时已经有所介绍了，ROS中的地图其实就是一张图片，这张图片有宽度、高度、分辨率等元数据，在图片中使用灰度值来表示障碍物存在的概率。不过SLAM构建的地图在导航中是不可以直接使用的，因为：

1. SLAM构建的地图是静态地图，而导航过程中，障碍物信息是可变的，可能障碍物被移走了，也可能添加了新的障碍物，导航中需要时时的获取障碍物信息；
2. 在靠近障碍物边缘时，虽然此处是空闲区域，但是机器人在进入该区域后可能由于其他一些因素，比如：惯性、或者不规则形体的机器人转弯时可能会与障碍物产生碰撞，安全起见，最好在地图的障碍物边缘设置警戒区，尽量禁止机器人进入...

所以，静态地图无法直接应用于导航，其基础之上需要添加一些辅助信息的地图，比如时时获取的障碍物数据，基于静态地图添加的膨胀区等数据。

**3.2组成**

代价地图有两张:global_costmap(全局代价地图) 和 local_costmap(本地代价地图)，前者用于全局路径规划，后者用于本地路径规划。

两张代价地图都可以多层叠加,一般有以下层级:

- Static Map Layer：静态地图层，SLAM构建的静态地图。
- Obstacle Map Layer：障碍地图层，传感器感知的障碍物信息。
- Inflation Layer：膨胀层，在以上两层地图上进行膨胀（向外扩张），以避免机器人的外壳会撞上障碍物。
- Other Layers：自定义costmap。

多个layer可以按需自由搭配。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E5%AF%BC%E8%88%AA%E9%9D%99%E6%80%81%E6%95%88%E6%9E%9C.png)

**3.3碰撞算法**

在ROS中，如何计算代价值呢？请看下图:

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E7%A2%B0%E6%92%9E%E7%AE%97%E6%B3%95.jpg)

上图中，横轴是距离机器人中心的距离，纵轴是代价地图中栅格的灰度值。

- 致命障碍:栅格值为254，此时障碍物与机器人中心重叠，必然发生碰撞；
- 内切障碍:栅格值为253，此时障碍物处于机器人的内切圆内，必然发生碰撞；
- 外切障碍:栅格值为[128,252]，此时障碍物处于其机器人的外切圆内，处于碰撞临界，不一定发生碰撞；
- 非自由空间:栅格值为(0,127]，此时机器人处于障碍物附近，属于危险警戒区，进入此区域，将来可能会发生碰撞；
- 自由区域:栅格值为0，此处机器人可以自由通过；
- 未知区域:栅格值为255，还没探明是否有障碍物。

膨胀空间的设置可以参考非自由空间。

**4.move_base使用**

路径规划算法在move_base功能包的move_base节点中已经封装完毕了，但是还不可以直接调用，因为算法虽然已经封装了，但是该功能包面向的是各种类型支持ROS的机器人，不同类型机器人可能大小尺寸不同，传感器不同，速度不同，应用场景不同....最后可能会导致不同的路径规划结果，那么在调用路径规划节点之前，我们还需要配置机器人参数。具体实现如下:

1. 先编写launch文件模板
2. 编写配置文件
3. 集成导航相关的launch文件
4. 测试

**4.1launch文件**

关于move_base节点的调用，模板如下:

```xml
<launch>

    <node pkg="move_base" type="move_base" respawn="false" name="move_base" output="screen" clear_params="true">
        <rosparam file="$(find 功能包)/param/costmap_common_params.yaml" command="load" ns="global_costmap" />
        <rosparam file="$(find 功能包)/param/costmap_common_params.yaml" command="load" ns="local_costmap" />
        <rosparam file="$(find 功能包)/param/local_costmap_params.yaml" command="load" />
        <rosparam file="$(find 功能包)/param/global_costmap_params.yaml" command="load" />
        <rosparam file="$(find 功能包)/param/base_local_planner_params.yaml" command="load" />
    </node>

</launch>
Copy
```

launch文件解释:

启动了 move_base 功能包下的 move_base 节点，respawn 为 false，意味着该节点关闭后，不会被重启；clear_params 为 true，意味着每次启动该节点都要清空私有参数然后重新载入；通过 rosparam 会载入若干 yaml 文件用于配置参数，这些yaml文件的配置以及作用详见下一小节内容。

**4.2配置文件**

关于配置文件的编写，可以参考一些成熟的机器人的路径规划实现，比如: turtlebot3，github链接：https://github.com/ROBOTIS-GIT/turtlebot3/tree/master/turtlebot3_navigation/param，先下载这些配置文件备用。

在功能包下新建 param 目录，复制下载的文件到此目录: costmap_common_params_burger.yaml、local_costmap_params.yaml、global_costmap_params.yaml、base_local_planner_params.yaml，并将costmap_common_params_burger.yaml 重命名为:costmap_common_params.yaml。

配置文件修改以及解释:

**4.2.1costmap_common_params.yaml**

该文件是move_base 在全局路径规划与本地路径规划时调用的通用参数，包括:机器人的尺寸、距离障碍物的安全距离、传感器信息等。配置参考如下:

```yaml
#机器人几何参，如果机器人是圆形，设置 robot_radius,如果是其他形状设置 footprint
robot_radius: 0.12 #圆形
# footprint: [[-0.12, -0.12], [-0.12, 0.12], [0.12, 0.12], [0.12, -0.12]] #其他形状

obstacle_range: 3.0 # 用于障碍物探测，比如: 值为 3.0，意味着检测到距离小于 3 米的障碍物时，就会引入代价地图
raytrace_range: 3.5 # 用于清除障碍物，比如：值为 3.5，意味着清除代价地图中 3.5 米以外的障碍物


#膨胀半径，扩展在碰撞区域以外的代价区域，使得机器人规划路径避开障碍物
inflation_radius: 0.2
#代价比例系数，越大则代价值越小
cost_scaling_factor: 3.0

#地图类型
map_type: costmap
#导航包所需要的传感器
observation_sources: scan
#对传感器的坐标系和数据进行配置。这个也会用于代价地图添加和清除障碍物。例如，你可以用激光雷达传感器用于在代价地图添加障碍物，再添加kinect用于导航和清除障碍物。
scan: {sensor_frame: laser, data_type: LaserScan, topic: scan, marking: true, clearing: true}
Copy
```

这里修改第一行的robot_radius：原型半径

最后一行的sensor_frame: laser雷达坐标系

**4.2.2global_costmap_params.yaml**

该文件用于全局代价地图参数设置:

```yaml
global_costmap:
  global_frame: map #地图坐标系
  robot_base_frame: base_footprint #机器人坐标系
  # 以此实现坐标变换

  update_frequency: 1.0 #代价地图更新频率
  publish_frequency: 1.0 #代价地图的发布频率
  transform_tolerance: 0.5 #等待坐标变换发布信息的超时时间

  static_map: true # 是否使用一个地图或者地图服务器来初始化全局代价地图，如果不使用静态地图，这个参数为false.
Copy
```

这里修改地图坐标系和机器人坐标系

**4.2.3local_costmap_params.yaml**

该文件用于局部代价地图参数设置:

```yaml
local_costmap:
  global_frame: odom #里程计坐标系
  robot_base_frame: base_footprint #机器人坐标系

  update_frequency: 10.0 #代价地图更新频率
  publish_frequency: 10.0 #代价地图的发布频率
  transform_tolerance: 0.5 #等待坐标变换发布信息的超时时间

  static_map: false  #不需要静态地图，可以提升导航效果
  rolling_window: true #是否使用动态窗口，默认为false，在静态的全局地图中，地图不会变化
  width: 3 # 局部地图宽度 单位是 m
  height: 3 # 局部地图高度 单位是 m
  resolution: 0.05 # 局部地图分辨率 单位是 m，一般与静态地图分辨率保持一致
Copy
```

这里修改里程计坐标系和机器人坐标系

**4.2.4base_local_planner_params**

基本的局部规划器参数配置，这个配置文件设定了机器人的最大和最小速度限制值，也设定了加速度的阈值。

```yaml
TrajectoryPlannerROS:

# Robot Configuration Parameters
  max_vel_x: 0.5 # X 方向最大速度
  min_vel_x: 0.1 # X 方向最小速速

  max_vel_theta:  1.0 # 
  min_vel_theta: -1.0
  min_in_place_vel_theta: 1.0

  acc_lim_x: 1.0 # X 加速限制
  acc_lim_y: 0.0 # Y 加速限制
  acc_lim_theta: 0.6 # 角速度加速限制

# Goal Tolerance Parameters，目标公差
  xy_goal_tolerance: 0.10
  yaw_goal_tolerance: 0.05

# Differential-drive robot configuration
# 是否是全向移动机器人
  holonomic_robot: false

# Forward Simulation Parameters，前进模拟参数
  sim_time: 0.8
  vx_samples: 18
  vtheta_samples: 20
  sim_granularity: 0.05
Copy
```

这个无需修改

**4.2.5参数配置技巧**

以上配置在实操中，可能会出现机器人在本地路径规划时与全局路径规划不符而进入膨胀区域出现假死的情况，如何尽量避免这种情形呢？

> 全局路径规划与本地路径规划虽然设置的参数是一样的，但是二者路径规划和避障的职能不同，可以采用不同的参数设置策略:
>
> - 全局代价地图可以将膨胀半径和障碍物系数设置的偏大一些；
> - 本地代价地图可以将膨胀半径和障碍物系数设置的偏小一些。
>
> 这样，在全局路径规划时，规划的路径会尽量远离障碍物，而本地路径规划时，机器人即便偏离全局路径也会和障碍物之间保留更大的自由空间，从而避免了陷入“假死”的情形。

**4.3launch文件集成**

如果要实现导航，需要集成地图服务、amcl 、move_base 与 Rviz 等，集成示例如下:

```xml
<launch>

    <!--地图服务-->
    <include file="$(find nav_demo)/launch/nav03_map_server.launch" />
    <!--amcl-->
    <include file="$(find nav_demo)/launch/nav04_amcl.launch" />
    <!--move_base-->
    <include file="$(find nav_demo)/launch/nav05_path.launch" />
    <!--rviz-->
    <node pkg="joint_state_publisher" name="joint_state_publisher" type="joint_state_publisher" />
    <node pkg="robot_state_publisher" name="robot_state_publisher" type="robot_state_publisher" />
    <node pkg="rviz" type="rviz" name="rviz" />

</launch>
```

**4.4测试**

1.先启动 Gazebo 仿真环境(此过程略)；

2.启动导航相关的 launch 文件；

3.添加Rviz组件(参考演示结果),可以将配置数据保存，后期直接调用；

全局代价地图与本地代价地图组件配置如下:

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/rviz%E4%BB%A3%E4%BB%B7%E5%9C%B0%E5%9B%BE.png)

全局路径规划与本地路径规划组件配置如下:

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/rviz%E8%B7%AF%E5%BE%84%E8%A7%84%E5%88%92.png)

4.通过Rviz工具栏的 2D Nav Goal设置目的地实现导航。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E5%AF%BC%E8%88%AA.gif)5.也可以在导航过程中，添加新的障碍物，机器人也可以自动躲避障碍物。







#### 7.2.5 导航与SLAM建图

> 场景:在 7.2.1 导航实现01_SLAM建图中，我们是通过键盘控制机器人移动实现建图的，而后续又介绍了机器人的自主移动实现，那么可不可以将二者结合，实现机器人自主移动的SLAM建图呢？

上述需求是可行的。虽然可能会有疑问，导航时需要地图信息，之前导航实现时，是通过 map_server 包的 map_server 节点来发布地图信息的，如果不先通过SLAM建图，那么如何发布地图信息呢？SLAM建图过程中本身就会时时发布地图信息，所以无需再使用map_server，SLAM已经发布了话题为 /map 的地图消息了，且导航需要定位模块，SLAM本身也是可以实现定位的。

该过程实现比较简单，步骤如下:

1. 编写launch文件，集成SLAM与move_base相关节点；
2. 执行launch文件并测试。

**1.编写launc文件**

当前launch文件实现，无需调用map_server的相关节点，只需要启动SLAM节点与move_base节点，示例内容如下:

```xml
<!--集成SLAM与导航，实现机器人自主移动的地图构建-->

<launch>
    
    <!--1.SLAM实现-->
    <include file="$(find nav_demo)/launch/nav01_slam.launch" />
    <!--2.导航中的move_base-->
    <include file="$(find nav_demo)/launch/nav05_path.launch" />


</launch>
```

**2.测试**

1.首先运行gazebo仿真环境；

2.然后执行launch文件；

3.在rviz中通过2D Nav Goal设置目标点，机器人开始自主移动并建图了；

4.最后可以使用 map_server 保存地图。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/%E8%87%AA%E4%B8%BB%E7%A7%BB%E5%8A%A8SLAM.gif)







上述公式稍显晦涩，PID控制原理框架图更有助于理解:

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/PID%E6%8E%A7%E5%88%B6.jpg)

##### 1.P
