参考视频链接：https://www.bilibili.com/video/BV1S5411X7FY/?spm_id_from=333.788.videopod.episodes&vd_source=10d7277f0ba446921a246233fba2160c

配套资料：链接:https://pan.baidu.com/s/1LHPX0NZuDyUqs7dsSZ8wjQ?pwd=5fok 提取码:5fok

# 一.前置知识：

## 1. python

人和计算机交互的一门编程语言



## 2. 库/包/package/library

别人分享的工具，安装包就用pip install 包名，具体的pip操作使用可以询问GPT得到解答



## 3. Pytorch/Tensorflow

就是python的库，安装可以使用pip install 包名



## 4. Anaconda

配置不同的虚拟环境



## 5. Pycharm

写代码的软件，配置一个项目的时候，需要配置好python解释器



## 6. 显卡GPU

显示图像，需要装驱动让计算机识别特定的硬件



## 7. CUDA

操作显卡的软件

![image-20241228183235328](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228183235328.png)

## 8. 环境配置中各软件之间的关系

![image-20241228183723020](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228183723020.png)

## 9. 判断有无GPU

打开任务管理器即可



# 二.Windows下安装Pytorch

## 1. 下载Anaconda

官网：https://www.anaconda.com/

安装成功后，可在菜单栏里看到命令行功能



## 2. 在Anaconda中配置虚拟环境

打开Anaconda中的Anaconda Prompt命令行，进行环境配置



1.查看现有的环境：

```shell
conda env list
```

![image-20241228185754217](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228185754217.png)

2.创建新的环境：

```
conda create -n 虚拟环境名 python=版本号
```

示例：

![image-20241228190207087](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228190207087.png)

其中的## Package Plan ##指的就是安装环境目录

安装成功后显示：

![image-20241228190325704](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228190325704.png)

第一行的意思是激活创建的这个环境

第二行的意思是退出这个环境

激活环境查看环境中的包有什么输入：

```
conda list
```

示例：

![image-20241228190604766](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228190604766.png)



## 3. 确定显卡算力，CUDA Driver版本和CUDA Runtime版本

CUDA runtime version <= CUDA driver version

CUDA runtime version 支持显卡对应的算力



进入网址：https://en.wikipedia.org/wiki/CUDA

根据自己的显卡型号确定算力和对应的CUDA版本，那我的举例：显卡型号：4060，对应算力8.9

![image-20241228193242131](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228193242131.png)

选择CUDA版本：12.0~12.5

![image-20241228193325288](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228193325288.png)

在命令行窗口输入nvidia-smi查看driver版本：可看到版本为12.6

![image-20241228193605738](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228193605738.png)

综上所述，我们可以使用安装12.5的CUDA版本，既满足算力需求，又满足Driver需求



## 4. 安装pytorch

进入pytorch官网：https://pytorch.org/

![image-20241228194300788](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228194300788.png)

复制下载命令行：

```
conda install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia
```

其中的pytorch torchvision torchaudio是一些包名，分别为核心包，图像包，语音包

**-c是通道的意思，如果下载速度慢可以在-c后面加镜像地址**

常用镜像地址：

```
清华镜像：https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/win-64/
```

1.进入想安装pytorch的环境中：

```
conda activate WangCeStudy
```

![image-20241228194802761](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228194802761.png)

2.输入安装指令：

```
conda install pytorch torchvision torchaudio pytorch-cuda=12.4 -c pytorch -c nvidia
```

![image-20241228194919929](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228194919929.png)



## 5.验证pytorch安装成功

1.激活对应环境：

```
conda activate 虚拟环境名
```

2.输入:

```
conda list
```

看看有没有pytorch或torch

3.输入 python 进入python环境中

输入import torch导包

输入torch.cuda.is_available()

如果返回true，则说明安装成功

![image-20241228200348432](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228200348432.png)

## 6. Pycharm中的环境配置

新建项目时可以在自定义环境中找到自己的python环境，如果没有的话去Anaconda/envs/虚拟环境名/python.exe

找到python.exe选中即可

![image-20241228201725727](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20241228201725727.png)

# 三.Jupyter Notebook打开步骤

1.打开Anaconda Prompt，切换到对应的运行环境，切换盘符并进入对应的文件夹，打开jupyter notebook即可

![image-20250207100902107](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250207100902107.png)