清空屏幕快捷键：crtl+l

使用ls -l查看文件时，前面的标注是d时是文件夹，是-时是文件

ctrl+c：强制停止命令的运行

# 一.Linux基础命令



## 1.Linux的目录结构

![image-20221027214128453](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027214128.png)

- `/`，根目录是最顶级的目录了
- Linux只有一个顶级目录：`/`
- 路径描述的层次关系同样适用`/`来表示
- /home/itheima/a.txt，表示根目录下的home文件夹内有itheima文件夹，内有a.txt



在Windows系统中，路径之间的层级关系，使用：`\`来表示

![image-20240821095713656](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821095713656.png)

在Windows中使用D:\data\work\hello.tst来表示



## 2.Linux命令基础格式

`command [-options] [parameter]`

- command：命令本身
- -options：[可选，非必填]命令的一些选项，可以通过选项控制命令的行为细节
- parameter：[可选，非必填]命令的参数，多数用于命令的指向目标等



## ls命令

功能：列出指定文件夹信息，没有指向时只需要列出当前工作目录下的内容

语法：`ls [-l -h -a] [参数]`

- 参数：被查看的文件夹，不提供参数，表示查看当前工作目录
- -l，以列表形式查看
- -h，配合-l，以更加人性化的方式显示文件大小
- -a，显示隐藏文件



**隐藏文件、文件夹**

在Linux中以`.`开头的，均是隐藏的。

默认不显示出来，需要`-a`选项才可查看到。

当不使用选项和参数，直接使用ls命令本体，表示：以平铺形式，列出当前工作目录下的内容

![image-20240821111426984](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821111426984.png)

显示根目录下的内容

![image-20240821111441105](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821111441105.png)

lh组合形式显示文件大小

![image-20240821111558625](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821111558625.png)





## pwd命令

功能：展示当前工作目录

语法：`pwd`

![image-20240821110848482](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821110848482.png)

## cd命令

功能：切换工作目录

语法：`cd [目标目录]`

参数：目标目录，要切换去的地方，不提供默认切换到`当前登录用户HOME目录`

![image-20240821110902511](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821110902511.png)



## HOME目录

每一个用户在Linux系统中都有自己的专属工作目录，称之为HOME目录。

- 普通用户的HOME目录，默认在：`/home/用户名`

- root用户的HOME目录，在：`/root`



FinalShell登陆终端后，默认的工作目录就是用户的HOME目录

## 相对路径、绝对路径

- 相对路径，==非==`/`开头的称之为相对路径

  相对路径表示以`当前目录`作为起点，去描述路径，如`test/a.txt`，表示当前工作目录内的test文件夹内的a.txt文件

- 绝对路径，==以==`/`开头的称之为绝对路径

  绝对路径从`根`开始描述路径



绝对路径写法：`cd /home/itheima/Desktop`

![image-20240821112636316](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821112636316.png)

相对路径写法：`cd Dexktop`

![image-20240821112739255](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821112739255.png)



## 特殊路径符

- `.`，**一个点**表示==当前目录==，比如./a.txt，表示当前文件夹内的`a.txt`文件
- `..`，**两个点**表示==上级目录==，比如`../`表示上级目录，`../../`表示上级的上级目录
- `~`，**一个波浪号**表示用户的==HOME目录==，比如`cd ~`，即可切回用户HOME目录



```
习题：
当前工作目录内有一个test文件夹，文件夹内有一个文件hello.txt，请描述文件的相对路径
test/hello.txt
在当前工作目录的上级目录有一个test文件夹，文件夹内有一个文件hello.txt，请描述文件的相对路径
../test/hello.txt
在HOME目录内有一个test文件夹，文件夹内有一个文件hello.txt，请描述文件的路径，需要使用符号~
~/test/hello.txt
```



## mkdir命令

功能：创建==文件夹==

语法：`mkdir [-p] 参数`

- 参数：被创建文件夹的路径
- 选项：-p，可选，表示创建前置路径

![image-20240821121338831](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821121338831.png)



![image-20240821121348172](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821121348172.png)



## touch命令

功能：创建==文件==

语法：`touch 参数`

- 参数：被创建的文件路径

![image-20240821122614934](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821122614934.png)

## cat命令

功能：查看==文件内容==

语法：`cat 参数`

- 参数：被查看的文件路径

![image-20240821122635410](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821122635410.png)

## more命令

功能：==查看文件==，可以==支持翻页==查看

语法：`more 参数`

- 参数：被查看的文件路径
- 在查看过程中：
  - `空格`键翻页
  - `q`退出查看



## cp命令

功能：复制文件、文件夹

语法：`cp [-r] 参数1 参数2`

- 参数1，被复制的
- 参数2，要复制去的地方
- 选项：-r，可选，复制文件夹使用

示例：

- cp a.txt b.txt，复制当前目录下a.txt为b.txt

  ![image-20240821125304400](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125304400.png)

- cp a.txt test/，复制当前目录a.txt到test文件夹内

- cp -r test test2，复制文件夹test到当前文件夹内为test2存在

![image-20240821125310021](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125310021.png)

## mv命令

功能：移动文件、文件夹

语法：`mv 参数1 参数2`

- 参数1：被移动的
- 参数2：要移动去的地方，参数2如果不存在，则会进行改名

![image-20240821125340324](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125340324.png)



![image-20240821125347682](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125347682.png)

## rm命令

功能：删除文件、文件夹

语法：`rm [-r -f] 参数...参数`

- 参数：支持多个，每一个表示被删除的，空格进行分隔
- 选项：-r，删除文件夹使用
- 选项：-f，强制删除，不会给出确认提示，一般root用户会用到



> rm命令很危险，一定要注意，特别是切换到root用户的时候。

删除文件：

![image-20240821125423722](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125423722.png)

删除多个文件：

![image-20240821125504491](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125504491.png)

删除文件夹：

![image-20240821125520326](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125520326.png)

**rm删除文件、文件夹-通配符**

rm命令支持==通配符== *，用来做==模糊匹配==

- 符号* 表示通配符，即匹配任意内容（包含空），示例：

- test*，表示匹配任何以test开头的内容

- *test，表示匹配任何以test结尾的内容

- *test *，表示匹配任何包含test的内容

![image-20240821125655812](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821125655812.png)



## which命令

功能：==查看命令==的程序本体文件路径

语法：`which 参数`

- 参数：被查看的命令

![image-20240821131451741](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821131451741.png)



## find命令

功能：==搜索文件==

语法1：按文件名搜索：`find 路径 -name 参数`

- 路径，搜索的起始路径
- 参数，搜索的关键字，支持通配符*， 比如：`*`test表示搜索任意以test结尾的文件

![image-20240821131738474](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821131738474.png)

**find命令-通配符**

find命令支持==通配符== *，用来做==模糊查询==

- 符号* 表示通配符，即匹配任意内容（包含空），示例：

- test*，表示匹配任何以test开头的内容

- *test，表示匹配任何以test结尾的内容

- *test *，表示匹配任何包含test的内容



![image-20240821131949085](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821131949085.png)



语法2：按文件大小搜索：`find 起始路径 -size +|- n[kMG]`

示例：

- 查找小于10KB的文件： find / -size -10k

- 查找大于100MB的文件：find / -size +100M

- 查找大于1GB的文件：find / -size +1G



## grep命令

功能：==过滤关键字==

语法：`grep [-n] 关键字 文件路径`

- 选项-n，可选，表示==在结果中显示==匹配的行的==行号==。
- 关键字，必填，表示过滤的关键字，带有空格或其它特殊符号，建议使用==””(双引号)==将关键字包围起来
- 文件路径，必填，表示要过滤内容的文件路径，可作为内容输入端口

> 参数文件路径，可以作为管道符的输入

![image-20240821134226470](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134226470.png)



![image-20240821134220087](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134220087.png)



## wc命令

功能：统计文件的==行数、字节数、单词数量==等

语法：`wc [-c -m -l -w] 文件路径`

- 选项，-c，统计bytes数量
- 选项，-m，统计字符数量
- 选项，-l，统计行数
- 选项，-w，统计单词数量
- 参数，文件路径，被统计的文件，可作为内容输入端口



> 参数文件路径，可作为管道符的输入



![image-20240821134246457](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134246457.png)



![image-20240821134304771](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134304771.png)



## 管道符|

写法：`|`

功能：将符号左边的结果，作为符号右边的输入

示例：

`cat a.txt | grep itheima`，将cat a.txt的结果，作为grep命令的输入，用来过滤`itheima`关键字

![image-20240821134355972](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134355972.png)

可以支持嵌套：

`cat a.txt | grep itheima | grep itcast`

![image-20240821134542998](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821134542998.png)



## echo命令

功能：输出内容

语法：`echo 参数`

- 参数：被输出的内容

![image-20240821145211290](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145211290.png)

## `反引号

功能：被两个反引号包围的内容，会作为命令执行

示例：

- echo \`pwd\`，会输出当前工作目录

![image-20240821145219202](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145219202.png)

## tail命令

功能：查看文件尾部内容

语法：`tail [-f，-num] 参数`

- 参数：被查看的文件
- 选项：-f，持续跟踪文件修改
- 选项：-num，表示查看尾部多少行，不填默认10行

![image-20240821145410009](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145410009.png)



![image-20240821145422167](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145422167.png)



## head命令

功能：查看文件头部内容

语法：`head [-n] 参数`

- 参数：被查看的文件
- 选项：-n，查看的行数



## 重定向符

功能：将符号左边的结果，输出到右边指定的文件中去

- `>`，表示覆盖输出
- `>>`，表示追加输出

![image-20240821145233070](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145233070.png)



![image-20240821145236300](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821145236300.png)

## Vim编辑器

![image-20240821152233093](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821152233093.png)

### 命令模式快捷键

![image-20221027215841573](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215841.png)

![image-20221027215846581](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215846.png)

![image-20221027215849668](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215849.png)

### 底线命令快捷键

![image-20221027215858967](https://image-set.oss-cn-zhangjiakou.aliyuncs.com/img-out/2022/10/27/20221027215858.png)



# 二.用户和权限

## 1.认识root用户

语法：`su [-] [用户名]`

常用语句:`su - root`

此时用户权限将会被切换为管理员权限

如果想使用sudo可以看下第3章的PPT

如果想退出root用户权限，可以使用快捷键==ctrl+d==或者==exit命令==

## 2.用户、用户组管理

1.Linux系统中可以：

- 配置多个用户
- 配置多个用户组
- 用户可以加入多个用户组中

2.Linux中关于权限的管控级别有2个权限，分别是：

- 针对用户的权限控制
- 针对用户组的权限控制

![image-20240821164118335](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821164118335.png)

针对某文件，可以控制用户的权限，也可以控制用户组的权限

以下命令需要root用户执行

3.用户组管理：

- 创建用户组：`groupadd 用户组名`

- 删除用户组：`groupdel 用户组名`

4.用户管理：

- 创建用户：useradd [-g -d]用户名

  - 选项：-g指定用户的组，不指定-g，会创建同名组并自动加入，指定-g需要组已经存在，如已存在同名组，必须使用-g

  - 选项：选项：-d指定用户HOME路径，不指定，HOME目录默认在：/home/用户名

- 删除用户：userdel [-r] 用户名
  - 选项：-r，删除用户的HOME目录，不使用-r，删除用户时，HOME目录保留

- 查看用户所属组：id [用户名]
  - 参数：用户名，被查看的用户，如果不提供则查看自身
- 修改用户所属组：usermod -aG 用户组 用户名
  - 将指定用户加入指定用户组



5.查看当前系统中有哪些用户：

语法：`getent passwd`

![image-20240821164814012](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821164814012.png)

共有7份信息，分别是：

用户名:密码(x):用户ID:组ID:描述信息(无用):HOME目录:执行终端(默认bash)

6.查看当前系统中有哪些用户组：

语法：`getent group`

![image-20240821164849898](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821164849898.png)

包含3份信息，组名称:组认证(显示为x):组ID



## 3.查看权限控制

1.通过ls -l可以以列表形式查看内容，并显示权限细节

![image-20240821173412767](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821173412767.png)

- 序号1：表示文件、文件夹的权限控制信息
- 序号2：表示文件、文件夹所属用户
- 序号3：表示文件、文件夹所属用户组

认知权限信息：

![image-20240821173554504](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240821173554504.png)



- r表示读权限

- w表示写权限

- x表示执行权限

针对文件、文件夹的不同，rwx的含义有细微差别

r：针对文件可以查看文件内容

​      针对文件夹，可以查看文件夹内容，如ls命令

w：针对文件表示可以修改此文件

​       针对文件夹，可以在文件夹内：创建、删除、改名等操作

x：针对文件表示可以将文件作为程序执行

​      针对文件夹，表示可以更改工作目录到此文件夹，即cd进入



## 4.修改权限控制 - chmod

1.可以使用chmod命令，修改文件、文件夹的==权限信息==

注意：只有文件、文件夹的所属用户或root用户可以修改

语法：`chmod [-R] 权限 文件或文件夹`

- -R，对文件夹内的全部内容应用同样的操作



2.示例：

- `chmod u=rwx,g=rx,o=x hello.txt`
  - 其中：u表示user所属用户权限，g表示group组权限，o表示other其它用户权限

快捷写法：

- `chmod 751 hello.txt`

![9a85c2b442cb283e8b6c7dacdcf860e8](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/9a85c2b442cb283e8b6c7dacdcf860e8.png)

## 5.修改权限控制 - chown

1.使用chown命令，可以修改文件、文件夹的所属==用户和用户组==

注意：此命令只适用于root用户执行

语法：`chown [-R] [用户][:][用户组] 文件或文件夹`

- -R：同chmod，对文件夹内全部内容应用相同规则

- 用户：修改所属用户

- 用户组：修改所属用户组

- :用于分隔用户和用户组



示例：

- chown root hello.txt，将hello.txt所属用户修改为root

- chown :root hello.txt，将hello.txt所属用户组修改为root

- chown root:itheima hello.txt，将hello.txt所属用户修改为root，用户组修改为itheima

- chown -R root test，将文件夹test的所属用户修改为root并对文件夹内全部内容应用同样规则



# 三.Linux实用操作

## 各类小技巧(快捷键)

**crtl+c强制停止**

![image-20240822100644284](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822100644284.png)

**crtl+d退出或登出**

![image-20240822100709891](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822100709891.png)

**history历史命令搜索**

![image-20240822100728688](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822100728688.png)



**通过!前缀，自动执行上一次匹配前缀的命令**

![image-20240822100751861](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822100751861.png)

**ctrl+r历史命令搜索，输入内容去匹配历史命令**

![image-20240822100821625](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822100821625.png)

**光标移动快捷键**

- ctrl + a，跳到命令开头

- ctrl + e，跳到命令结尾

- ctrl + 键盘左键，向左跳一个单词

- ctrl + 键盘右键，向右跳一个单词



**清屏**

- 通过快捷键ctrl + l，可以清空终端内容

- 或通过命令clear得到同样效果



## 软件安装

安装软件时的格式：

CentOs：rpm、yum

语法：`yum [-y] [install | remove |search] 软件名称`

![image-20240822102530965](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822102530965.png)

Ubuntu：deb、apt

语法：`apt [-y] [install | remove |search] 软件名称`



## Systemctl

Linux系统很多软件(内置或第三方)均支持使用systemctl命令控制：启动、停止、开机自启

能够被systemctl管理的软件，一般也称之为：服务

语法：`systemctl start | stop | status | enable |disable 服务名`

- start 启动

- stop 关闭

- status 查看状态

- enable 开启开机自启

- disable 关闭开机自启

部分第三方软件安装后也可以以systemctl进行控制



## ln命令创建软链接

在系统中创建软链接，可以将文件、文件夹连接到其它位置

语法：`ln -s 参数1 参数2`

- -s选项，创建软连接

- 参数1：被链接的文件或文件夹

- 参数2：要链接去的目的地



## 日期、时区(没看)



## IP地址和主机名

IP地址主要有两个版本：V4版本和V6版本

IPV4版本的地址格式是：a.b.c.d，其中abcd表示0~255的数字，比如192.168.88.101就是一个标志的IP地址

可以通过命令：ifconfig查看本机的ip地址



**特殊的IP地址**：

127.0.0.1：这个IP地址用于指代本机

0.0.0.0：

- 可以用于指代本机

- 可以在端口绑定中用来确定绑定关系（后续讲解）

- 在一些IP地址限制中，表示所有IP的意思，如放行规则设置为0.0.0.0，表示允许任意IP访问



**主机名**：可以使用hostname查看主机名

可以使用命令：`hostnamectl set-hostname`修改主机名(需要root权限)



**域名解析**：配置主机名映射(参考视频)



![image-20240822122816307](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822122816307.png)

**配置虚拟机的固定IP(没看)**



## 网络请求和下载



**ping命令**：可以通过ping命令，检查指定的网络服务器是否是可联通状态

语法：`ping [-c num] ip或主机名`

- -c：检查的次数，不使用-c选项，将无限次数持续检查

- ip或主机名：被检查的服务器的ip地址或主机名地址

检查到39.156.66.10是否联通，并检查3次

![image-20240822124834911](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822124834911.png)



**wget命令**：wget是非交互式的文件下载器，可以在命令行内下载网络文件

语法：`wget [-b] url`

- -b：可选，后台下载，会将日志写入到当前工作目录的wget-log文件

- url：下载链接



![image-20240822125011406](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822125011406.png)



**curl命令**：curl可以发送http网络请求，可用于：下载文件、获取信息等

语法：`curl [-0] ur1`

- -O：用于下载文件，当url是下载链接时，可以使用此选项保存文件

- url：要发起请求的网络地址



![image-20240822125618958](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822125618958.png)



## 端口

端口，是设备与外界通讯交流的出入口。端口可以分为：物理端口和虚拟端口两类

- 物理端口：又可称之为接口，是可见的端口，如USB接口，RJ45网口，HDMI端口等

- 虚拟端口：是指计算机内部的端口，是不可见的，是用来操作系统和外部进行交互使用的

![image-20240822130845894](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822130845894.png)



![image-20240822130849559](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822130849559.png)



IP地址相当于小区地址，在小区内可以有许多住户（程序），而门牌号（端口）就是各个住户（程序）的联系地址

![image-20240822130928856](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822130928856.png)



### 使用nmap命令查看IP地址：

语法：`namp 被查看的IP地址`

![image-20240822131138053](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822131138053.png)



### 使用netstat命令，查看指定端口的占用情况：

语法：`netstat -anp | grep 端口号`

![image-20240822131537296](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822131537296.png)



## 进程管理

程序运行在操作系统中，是被操作系统所管理的。

为管理运行的程序，每一个程序在运行的时候，便被操作系统注册为系统中的一个：进程

并会为每一个进程都分配一个独有的：进程ID（进程号）

![image-20240822133239153](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133239153.png)



![image-20240822133242662](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133242662.png)





### **查看进程：**可以通过ps命令查看Linux系统中的进程信息

语法：`ps [-e -f]`

- -e：显示出全部的进程

- -f：以完全格式化的形式展示信息（展示全部信息）

一般来说，固定用法就是：ps -ef 列出全部进程的全部信息

![image-20240822133411550](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133411550.png)



**从左到右分别是：**

- UID：进程所属的用户ID

- PID：进程的进程号ID

- PPID：进程的父ID（启动此进程的其它进程）

- C：此进程的CPU占用率（百分比）

- STIME：进程的启动时间

- TTY：启动此进程的终端序号，如显示?，表示非终端启动

- TIME：进程占用CPU的时间

- CMD：进程对应的名称或启动路径或启动命令

也可以使用grep和管道符|来配合使用

![image-20240822133849662](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133849662.png)



### **关闭进程：**通过kill命令关闭进程

语法：`kill [-9] 进程ID`

- -9：表示强制关闭进程。不使用此选项会向进程发送信号要求其关闭，但是否关闭看进程自身的处理机制。



![image-20240822133857893](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133857893.png)



![image-20240822133907990](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822133907990.png)





## 主机状态



**1.查看系统资源占用：**通过top命令查看CPU、内存使用情况，类似Windows的任务管理器，默认每5s刷新一次

语法：`top`



![image-20240822140931256](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822140931256.png)





- 第一行：

![image-20240822141016310](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141016310.png)

top：命令名称，14:39:58：当前系统时间，up 6 min：启动了6分钟，2 users：2个用户登录，load：1、5、15分钟负载

- 第二行：

![image-20240822141021894](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141021894.png)

Tasks：175个进程，1 running：1个进程子在运行，174 sleeping：174个进程睡眠，0个停止进程，0个僵尸进程

- 第三行：

![image-20240822141026798](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141026798.png)

%Cpu(s)：CPU使用率，us：用户CPU使用率，sy：系统CPU使用率，ni：高优先级进程占用CPU时间百分比，id：空闲CPU率，wa：IO等待CPU占用率，hi：CPU硬件中断率，si：CPU软件中断率，st：强制等待占用CPU率

- 第四、五行：

![image-20240822141030770](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141030770.png)

Kib Mem：物理内存，total：总量，free：空闲，used：使用，buff/cache：buff和cache占用

KibSwap：虚拟内存（交换空间），total：总量，free：空闲，used：使用，buff/cache：buff和cache占用



top命令内容详解：

![image-20240822141111048](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141111048.png)



- PID：进程id

- USER：进程所属用户

- PR：进程优先级，越小越高

- NI：负值表示高优先级，正表示低优先级

- VIRT：进程使用虚拟内存，单位KB

- RES：进程使用物理内存，单位KB

- SHR：进程使用共享内存，单位KB

- S：进程状态（S休眠，R运行，Z僵死状态，N负数优先级，I空闲状态）

- %CPU：进程占用CPU率

- %MEM：进程占用内存率

- TIME+：进程使用CPU时间总计，单位10毫秒

- COMMAND：进程的命令或名称或程序文件路径



top命令也支持选项：

![image-20240822141616009](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141616009.png)





使用完top命令后，可以在界面使用快捷键功能：

![image-20240822141636020](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141636020.png)



**2.磁盘信息监控：**使用df命令，可以查看磁盘的使用情况

语法：`df [-h]`

- -h：以更加人性化的单位显示

![image-20240822141812152](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141812152.png)





**3.可以使用iostat查看CPU、磁盘的相关信息**

语法：`iostat [-x] [num1] [num2]`

- -x：显示更多信息

- num1：刷新间隔(s)
- num2：刷新几次

![image-20240822141959108](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822141959108.png)



rrqm/s： 每秒这个设备相关的读取请求有多少被Merge了（当系统调用需要读取数据的时候，VFS将请求发到各个FS，如果FS发现不同的读取请求读取的是相同Block的数据，FS会将这个请求合并Merge, 提高IO利用率, 避免重复调用）；

wrqm/s： 每秒这个设备相关的写入请求有多少被Merge了。

rsec/s： 每秒读取的扇区数；sectors

wsec/： 每秒写入的扇区数。

rKB/s： 每秒发送到设备的读取请求数

wKB/s： 每秒发送到设备的写入请求数

avgrq-sz  平均请求扇区的大小

avgqu-sz  平均请求队列的长度。毫无疑问，队列长度越短越好。  

await：  每一个IO请求的处理的平均时间（单位是微秒毫秒）。

svctm   表示平均每次设备I/O操作的服务时间（以毫秒为单位）

%util：  磁盘利用率



**4.网络状态监控：**可以使用sar命令查看网络的相关统计（sar命令非常复杂，这里仅简单用于统计网络）

语法：`sar -n DEV num1 num2`

- -n：查看网络，DEV表示查看网络接口

- num1：刷新间隔（不填就查看一次结束）
- num2：查看次数（不填无限次数）

![image-20240822142126460](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822142126460.png)



信息解读：

- IFACE 本地网卡接口的名称

- rxpck/s 每秒钟接受的数据包

- txpck/s 每秒钟发送的数据包

- rxKB/S 每秒钟接受的数据包大小，单位为KB

- txKB/S 每秒钟发送的数据包大小，单位为KB

- rxcmp/s 每秒钟接受的压缩数据包

- txcmp/s 每秒钟发送的压缩包

- rxmcst/s 每秒钟接收的多播数据包





## 环境变量

环境变量是操作系统(Windows\Linux\Mac)在运行的时候，记录的一些关键性信息，用以辅助系统运行。

**1.在Linux系统中执行：==env命令==即可查看当前系统中记录的环境变量**

环境变量是一种KeyValue型结构，即名称和值，如下图：



![image-20240822145920081](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822145920081.png)



**2.环境变量：PATH**

在前面提出的问题中，我们说无论当前工作目录是什么，都能执行/usr/bin/cd这个程序，这个就是借助环境变量中：PATH这个项目的值来做到的。

![image-20240822150214905](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822150214905.png)



PATH记录了系统执行任何命令的搜索路径，如上图记录了（路径之间以:隔开）：

- /usr/local/bin

- /usr/bin

- /usr/local/sbin

- /usr/sbin

- /home/itheima/.local/bin

- /home/itheima/bin

当执行任何命令，都会按照顺序，从上述路径中搜索要执行的程序的本体，比如执行cd命令，就从第二个目录/usr/bin中搜索到了cd命令，并执行



**3.$符号：**

在Linux系统中，$符号被用于取”变量”的值。环境变量记录的信息，除了给操作系统自己使用外，如果我们想要取用，也可以使用。

取得环境变量的值就可以通过语法：`$环境变量名`来取得

比如： echo $PATH

![image-20240822150516859](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822150516859.png)

又或者：echo ${PATH}ABC	当和其他内容混合在一起的时候，可以通过{}来标注取的变量是谁

![image-20240822150555278](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822150555278.png)



**4.自行设置环境变量：**

Linux环境变量可以用户自行设置，其中分为：

- 临时设置，语法：`export 变量名=变量值`

- 永久生效
  - 针对当前用户生效，配置在当前用户的： ~/.bashrc文件中
  - 针对所有用户生效，配置在系统的： /etc/profile文件中
  - 并通过语法：source 配置文件，进行立刻生效，或重新登录FinalShell生效



1）临时配置：

![image-20240822150808672](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822150808672.png)

2）针对当前用户生效：

- 使用vi编辑器进去当前用户的~/.bashrc文件中编辑

![fe418cdf694929117e41c1c2ddaf6e77](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/fe418cdf694929117e41c1c2ddaf6e77.png)

- 在结尾的末端加上想要加的语句，这里是`export MYNAME=itheima`

![ade13013f34bd030fe76ffe99f276201](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/ade13013f34bd030fe76ffe99f276201.png)

- 使用source配置文件，此时对于ros用户MYNAME的值将永久是itheima

![db05f0fcb74c9dfc573d231fba5f5313](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/db05f0fcb74c9dfc573d231fba5f5313.png)

3）针对所有用户生效：

- 上述语法当用户转为root用户时，MYNAME将无法等同于itheima

![ce42edf7cc101bfadfdbc457d11b3384](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/ce42edf7cc101bfadfdbc457d11b3384.png)

- 为了使所有用户都可以使用，需要修改系统中的/etc/profile文件

![379eaf447b0892eeebcaf3add13e5d95](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/379eaf447b0892eeebcaf3add13e5d95.png)

- 打开文件并修改保存后使用source即可完成环境的配置

![e2db8f63a0088bea113dc89e936ba2ff](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e2db8f63a0088bea113dc89e936ba2ff.png)









**5.自定义环境变量PATH**

1）创建mkenv文件夹并进入：

![7c5df2035c6ac684ff09b800af6e88ab](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/7c5df2035c6ac684ff09b800af6e88ab.png)

2）使用vim编辑器编写内容为：`echo = "哈哈哈"`

![9a81300c455455e7d8644943a3998507](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/9a81300c455455e7d8644943a3998507.png)

3）给文件mkhaha权限755：

![29bb4c972916fd3b94c28c494aea443f](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/29bb4c972916fd3b94c28c494aea443f.png)

4）为了让文件在所有区域都能被找到，需要使用root权限修改/etc/profile文件：

![eab243c22d4b9da07e7f0d212c71158c](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/eab243c22d4b9da07e7f0d212c71158c.png)

5）将文件目录添加进PATH中：

![0d511364b50838c596e84c71c41c2799](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/0d511364b50838c596e84c71c41c2799.png)

6）保存后source一下，可以看出来前后对比：

![eea3012c3bfdbd3429e5f50656cdebe6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/eea3012c3bfdbd3429e5f50656cdebe6.png)

PATH路径中添加了一个新的路径

![276b49796c42d06bb9d405101cc5edab](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/276b49796c42d06bb9d405101cc5edab.png)

7）这样在别的目录下输出mkhaha时也会显示具体数值：

![536062b661dd1a8211f8c896c53baea6](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/536062b661dd1a8211f8c896c53baea6.png)







## 上传、下载

1.直接拖拽即可

2.使用rz或sz命令：

- rz命令，进行上传，语法：直接输入rz即可

![image-20240822152837176](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822152837176.png)

- sz命令进行下载，语法：sz 要下载的文件

![image-20240822152843610](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20240822152843610.png)

为了获得最大权限，需要使用root账户登录才能在下面显示root文件夹下的内容





## 压缩、解压

### 1.市面上有非常多的压缩格式：

- zip格式：Linux、Windows、MacOS，常用

- 7zip：Windows系统常用

- rar：Windows系统常用

- tar：Linux、MacOS常用

- gzip：Linux、MacOS常用

### 2.tar命令

1.Linux和Mac系统常用有2种压缩格式，后缀名分别是：

- .tar，称之为tarball，归档文件，即简单的将文件组装到一个.tar的文件内，并没有太多文件体积的减少，仅仅是简单的封装

- .gz，也常见为.tar.gz，gzip格式压缩文件，即使用gzip压缩算法将文件压缩到一个文件内，可以极大的减少压缩后的体积

针对这两种格式，使用tar命令均可以进行压缩和解压缩的操作

2.语法：`tar [-c -v -x -f -z -C] 参数1 参数2 ... 参数N`

- -c，创建压缩文件，用于压缩模式

- -v，显示压缩、解压过程，用于查看进度

- -x，解压模式

- -f，要创建的文件，或要解压的文件，-f选项必须在所有选项中位置==处于最后一个==

- -z，gzip模式，不使用-z就是普通的tarball格式

- -C，选择解压的目的地，用于解压模式



3.tar命令压缩：

tar的常用组合为：

- tar -cvf test.tar 1.txt 2.txt 3.txt
  - 将1.txt 2.txt 3.txt 压缩到test.tar文件内

- tar -zcvf test.tar.gz 1.txt 2.txt 3.txt
  - 将1.txt 2.txt 3.txt 压缩到test.tar.gz文件内，使用gzip模式



4.tar命令解压：

常用的tar解压组合有

- tar -xvf test.tar
  - 解压test.tar，将文件解压至当前目录

- tar -xvf test.tar -C /home/itheima
  - 解压test.tar，将文件解压至指定目录（/home/itheima）

- tar -zxvf test.tar.gz -C /home/itheima
  - 以Gzip模式解压test.tar.gz，将文件解压至指定目录（/home/itheima）



5.注意：

- -f选项，必须在选项组合体的最后一位

- -z选项，建议在开头位置

- -C选项单独使用，和解压所需的其它参数分开



### 3.zip命令压缩文件

1.压缩文件：

可以使用zip命令，压缩文件为zip压缩包

语法：`zip [-r] 参数1 参数2 ... 参数N`

- -r：被压缩的包含文件夹的时候，需要使用-r选项，和rm、cp等命令的-r效果一致



示例：

- zip test.zip a.txt b.txt c.txt
  - 将a.txt b.txt c.txt 压缩到test.zip文件内

- zip -r test.zip test itheima a.txt
  - 将test、itheima两个文件夹和a.txt文件，压缩到test.zip文件内





### 4.unzip命令解压文件



1.使用unzip命令，可以方便的解压zip压缩包

语法：`unzip [-d] 参数`

- -d，指定要解压去的位置，同tar的-C选项

- 参数，被解压的zip压缩包文件



示例：

- unzip test.zip，将test.zip解压到当前目录

- unzip test.zip -d /home/itheima，将test.zip解压到指定文件夹内（/home/itheima）









