# 一.YOLO v1

参考链接：

https://www.bilibili.com/video/BV1LK411973P/?spm_id_from=333.788.player.switch&vd_source=10d7277f0ba446921a246233fba2160c&p=2

https://jrs0511.blog.csdn.net/article/details/129011644

## 0.Abstract

YOLO是一个新的目标检测方式，过去的目标检测会经历two-stage阶段，而yolo只需要one-stage，将过去的分类与边框预测问题，转化为回归问题

![image-20250526111033780](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526111033780.png)

YOLO在全局图像上识别物体，可以使用全局信息来判断，而过去的只是在特定框内判断是否为物体

![image-20250526111306244](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526111306244.png)

由于yolo是一个单独的网络，所以能够直接优化,能够实现端到端(end-to-end)的优化

YOLO框架的统一性使得系统的检测速度非常快，能够达到45FPS，与sota相比，yolo定位错误多但是背景误判少。YOLO的通用性强，对于艺术作品也可以识别出人，明显优于DPM和RCNN网络。==(DPM和RCNN是啥？)==

![image-20250526111355443](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526111355443.png)

## 1.Introduction

像DMP这样的系统第一阶段使用滑动窗口方法来确定位置，第二阶段使用卷积来分类

像R-CNN这样的方法首先在图像上生成潜在的框，然后在这些目标框内使用分类器确定种类

这种两步走的方法是很慢的而且很难优化的，YOLO直接从图片像素--->生成框的坐标和物体类别，这样做yolo有几个优点：

- YOLO是非常快的
- 使用图片的全局信息进行推理
- 泛化能力强

![image-20250604093527796](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250604093527796.png)





## 2.Unified Detection

yolo将图片分为S x S 个格子，如果一个物体的中心落入一个单元格内，那么这个单元格负责检测那个物体

- 训练阶段，网络通过真实的物体中心点和标注的信息，计算损失并更新权重，使得预测的边界框和类别越来越准确
- 推理阶段：对于新图像，网络会按照已经学习到的参数，预测图像中的物体位置(边界框)和类别，最终生成物体的框和标签

每个单元格预测B个框和这些框的置信度分数

![image-20250526181309712](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181309712.png)

Pr(Object)：没有预测目标=0；有预测目标=1；

IOU=交并比

![image-20250526181410308](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181410308.png)

置信度=Pr(Object) * IOU

![image-20250526181334344](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181334344.png)

每个框包含5个参数；x y w h 和置信度，一般前四个参数会归一化

![image-20250526181511526](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181511526.png)

归一化步骤：

![image-20250526181619444](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181619444.png)

每个格会预测C个类

![image-20250526181649555](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181649555.png)

**最后编码为S x S x (B * 5 + C)个张量**

![image-20250526181822263](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250526181822263.png)

前面10个信息分别为两个框的(x,y,w,h,c)，后面二十个是类别C的概率

==发现了一个问题：有可能置信度高但是类别错误，据说这个问题在后续的版本中被改进了==

### 2.1 Network Design

看网络的时候一般要注意以  下几点：

- 网络构造
- loss function
- 预处理

yolov1的网络结构如下：24个卷积层(不包含最大池化层)和2个全连接层

![image-20250527092325920](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250527092325920.png)

网络一般会分为卷积层和全连接层

- 卷积层：提取特征
- 全连接层：分类

1x1的网络通过降维的方式，达到了运算量的减少，最后网络的输出是7x7x30 tensor



### 2.2 Training

top5的含义：预测一个目标时，会有5个分类，如果正确的类别在预测的5个类别中，那么就说在top5中预测是正确的；

top1的含义：预测的排名第一的类别如果和真实类别相同，那么top1就是正确的

如下图，汽车的top1是正确的；大厦的top5是正确的，但是top1是错误的

![image-20250527111031102](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250527111031102.png)

模型的最后一层使用线性激活函数，而所有其它的层使用下面的Leaky-ReLU函数:
$$
\phi(x) =
\begin{cases} 
x, & \text{if } x > 0 \\
0.1x, & \text{otherwise}
\end{cases}
$$
使用平方和误差函数来优化模型，如果定位误差和分类误差是相同的，那么结果可能非常不理想，同时，许多格子是不包含物体的，这将导致格子的置信度为0，这会导致那些包含物体格子的梯度被压缩

为了解决这种问题，将包含对象的损失函数赋予高权重5，不包含对象的损失函数赋予低权重0.5

大框中的小偏差影响应该小于小框中的小偏差，所以我们使用平方根来代替宽度和高度值

在训练时，只留下IOU最大值的那个框

损失函数公式如下：可大致分为(定位损失、置信度损失、类别损失)
$$
\text{Loss} = \lambda_{\text{coord}} \sum_{i=0}^{S^2} \sum_{j=0}^{B} \mathbb{1}_{ij}^{\text{obj}} \Big[ (x_i - \hat{x}_i)^2 + (y_i - \hat{y}_i)^2 \Big] 
+ \lambda_{\text{coord}} \sum_{i=0}^{S^2} \sum_{j=0}^{B} \mathbb{1}_{ij}^{\text{obj}} \Big[ \Big(\sqrt{w_i} - \sqrt{\hat{w}_i} \Big)^2 + \Big(\sqrt{h_i} - \sqrt{\hat{h}_i} \Big)^2 \Big]
$$

$$
+ \sum_{i=0}^{S^2} \sum_{j=0}^{B} \mathbb{1}_{ij}^{\text{obj}} \Big( C_i - \hat{C}_i \Big)^2 
+ \lambda_{\text{noobj}} \sum_{i=0}^{S^2} \sum_{j=0}^{B} \mathbb{1}_{ij}^{\text{noobj}} \Big( C_i - \hat{C}_i \Big)^2
$$

$$
+ \sum_{i=0}^{S^2} \mathbb{1}_{i}^{\text{obj}} \sum_{c \in \text{classes}} \Big( p_i(c) - \hat{p}_i(c) \Big)^2
$$

超参数的设置：
batch size=64，momentum=0.9，decay=0.0005，learning rate=0.01，dropout=0.5，learning rate=0.01，数据增强，非极大值抑制







# 二.YOLO v2

参考链接：

https://www.bilibili.com/video/BV1NK41127TH/?spm_id_from=333.337.search-card.all.click&vd_source=10d7277f0ba446921a246233fba2160c

https://jrs0511.blog.csdn.net/article/details/129087464

## 0.Abstract

数据集的不同：

![image-20250609094301532](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250609094301532.png)

ImageNet数据集主要用来做分类任务，有近22000个类别；

PASCAL VOC和MS COCO数据集主要用来做检测，分别有20个种类和80个种类，种类较少



## 1.Introduction







## 2.Better

**精度和召回率的解析**：假设共有10张图片，其中有五张是飞机，这时将检测到的图片排序

- 精度：正确的占比
- 召回率：找回来几个

![image-20250610092205766](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250610092205766.png)

各种trick的效果：

![image-20250610095642207](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250610095642207.png)

### 2.1 Batch Normalization

CNN在训练过程中网络每层输入的分布一直在改变, 会使训练过程难度加大，对网络的每一层的输入(每个卷积层后)都做了归一化，**这样网络就不需要每层都去学数据的分布，收敛会更快**。

YOLOv2使用的批量归一化公式：
$$
\hat{x}_i = \frac{x_i - \mu_B}{\sqrt{\sigma_B^2 + \epsilon}}
$$

$$
y_i = \gamma \hat{x}_i + \beta
$$

其中：

- \( $x_i$ \) 是输入特征。
- \( $\mu_B$ \) 是当前 mini-batch 的均值：
  $$
  \mu_B = \frac{1}{m} \sum_{i=1}^m x_i
  $$
- \( $\sigma_B^2$ \) 是当前 mini-batch 的方差：
  $$
  \sigma_B^2 = \frac{1}{m} \sum_{i=1}^m (x_i - \mu_B)^2
  $$
- \($ \epsilon$ \) 是一个小的正值，用于避免除零。
- \($ \hat{x}_i$ \) 是标准化后的特征。
- \($ \gamma$ \) 和 \( $\beta $\) 是可学习的参数，用于恢复特征的表达能力。
- \( $y_i $\) 是最终的归一化输出。



使用批量归一化可以使模型收敛的更快、更准确



### 2.2 High Resolution Classifier

检测方法都使用在ImageNet上预先训练的分类器作为预训练模型。从AlexNet开始，大多数分类器的输入都小于256×256。

v1中预训练使用的是分类数据集，大小是224×224 ，然后迁移学习，微调时使用YOLO模型做目标检测的时候才将输入变成448 × 448。这样改变尺寸，网络就要多重新学习一部分，会带来性能损失。

v2直接在预训练中输入的就是**448×448**的尺寸，微调的时候也是**448 × 448**。使mAP增加了近4%

epoch的定义：

![image-20250610103817019](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250610103817019.png)



### 2.3 Convolutional With Anchor Boxes

**anchor box：**在yolov1预测框时，模型直接预测两个框；而如果使用anchor box，那么会在预测前，将5个框的大小进行预定义，优化时通过预定义的大小来进行优化



通过32倍下采样，使输出的特征图为13x13

![image-20250610111452464](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250610111452464.png)

最后的输出大小为13 * 13 * (5 * (4+1+20))=13x13x125，代表了5个框，每个框有4个坐标值，1个置信度，和20个类别值

![image-20250610111719364](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250610111719364.png)





|          | YOLOv1                                                       | YOLOv2                                                       |
| :------- | :----------------------------------------------------------- | ------------------------------------------------------------ |
| 初始位置 | 初始生成两个boxes，加大了学习复杂度。                        | Anchor初始是固定的，但在训练过程中会进行微调。使用Anchor boxes之后，每个位置的各个Anchor box都单独预测一组分类概率值。 |
| 输出公式 | (框数 * 信息数)+分类数                                       | 框数 *(信息数+分类数)                                        |
| 公式含义 | 在YOLOv1中，类别概率是由grid cell来预测的，每个cell都预测2个boxes，每个boxes包含5个值，每个grid cell 携带的是30个信息。但是每个cell只预测一组分类概率值，供2个boxes共享。 | 在YOLOv2中，类别概率是属于box的，每个box对应一个类别概率，而不是由cell决定，因此这边每个box对应25个预测值。每个grid cell携带的是 25 × 5 =125个信息，25是 xywh+置信度+分类数，5就是5个Anchor。 |
| 输出框   | 7 × 7 × 2 = 98个框                                           | 13 × 13 × 5 = 845个框                                        |
| 输出值   | 7 ×7 × 30                                                    | 13 × 13 × 5 × 25                                             |



![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/5ec3fbccf82e6e12aab0f72944f57751.png)

### 2.4 Dimension Clusters

使用Anchor Boxes的问题之一：尺寸是手工指定了长宽比和尺寸，相当于一个超参数，这违背了YOLO对于目标检测模型的初衷，**因为如果指定了Anchor的大小就没办法适应各种各样的物体了**。

在训练集的边界框上运行K-means聚类训练bounding boxes，可以自动找到更好的boxes宽高维度。由上面分析已知，设置先验Anchor Boxes的主要目的是为了使得预测框与真值的IOU更好，所以聚类分析时选用box与聚类中心box之间的IOU值作为距离指标

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/7ec474cf97227a315529f5fb4dc8f7a5.png)

欧式距离(Euclidean distance)：会产生错误

![image-20250616110424217](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250616110424217.png)

使用交并比来代替：d值越小，说明两个框越近

![image-20250616110626632](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250616110626632.png)



### 2.5 Direct location prediction

当使用anchor box时，会遇到第二个问题：模型的不稳定性，大多数的不稳定来自于预测框(x,y)的位置，传统的预测方式可能造成预测框逐渐产生偏移，最后离真实框过远，在训练时有三个框的概念：

- Ground Truth：数据集中标注的物体真实框
- 预测框：模型预测的物体所在位置框
- anchor：预测前的预选框，可以加强模型的推理能力

![image-20250702110749773](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250702110749773.png)

推理阶段简单来说，就是用anchor框推理预测框的位置，最后通过真实框来更新系统参数权重

![image-20250702111047526](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250702111047526.png)



公式如下：
$$
x = (t_x * w_a) - x_a
$$

$$
y = (t_y * h_a) - y_a
$$

由于公式受限制较少，预测框无论在哪儿开始，都可能在任何位置结束(出界)

我们使用新的公式，将坐标值限制在0~1之间，公式如下：
$$
b_x = \sigma(t_x) + c_x \\
b_y = \sigma(t_y) + c_y \\
b_w = p_w e^{l_w} \\
b_h = p_h e^{l_h}
$$

$$
Pr(\text{object}) * IOU(b, \text{object}) = \sigma(t_o)
$$

具体操作如下：

![image-20250702122902877](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250702122902877.png)

bx与by通过这种方式，会将值限制在0~1之间；bw和bh通过这种方式，杜绝了负值的出现

### 2.6 Fine-Grained Features

这个修改后的YOLO在13 × 13特征图上进行检测。虽然这对于大型对象来说已经足够了，但是对于较小的对象来说，更细粒度的特性可能会使得检测效果更好。

我们采取了一个不同于Fast R-CNN和SSD的方法，添加了一个直通层(passthrough)，它将26x26x512的特征图变为13x13x2048的特征图

![image-20250703091920118](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250703091920118.png)

与ResNet类似，直通层(passthrough)不采用空间平面组合的方式，而是采用堆叠的方式将通道组合在一起

ResNet原型：

![image-20250703092152642](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250703092152642.png)

passthrough的方式及原理：

![image-20250703092248780](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250703092248780.png)

检测器在扩展后的特征图上进行，这使得它可以访问细粒度的特征，这种方法，使性能有了1%的提升



### 2.7 Multi-Scale Training

yolov1的输入分辨率为448 x 448，v2的输入分辨率为416 x 416，是因为这两个算法都是使用32倍下采样，但v1的那个版本会导致下采样后的分辨率为14 x 14，出现偶数，为了防止出现偶数，v2修改为416 x 416



## 3.Faster

YOLO的定制化框架借鉴了GoogLeNet网络结构



### 3.1 Darknet-net

与VGG模型相似，我们主要使用3x3卷积，每次下采样后，卷积核个数翻倍

参考NIN网络，我们使用了全局平均池化进行预测、在卷积层之间使用了1x1卷积进行降维

我们使用batch normalization稳定训练、加速收敛、正则化网络

![image-20250704103853118](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250704103853118.png)

平均池化：

将整个图像池化为一个块儿

![image-20250717093423803](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250717093423803.png)

1x1卷积降维：

降维->升维->减少运算量

### 3.2 Training for classification

分类的训练 我们使用随机梯度下降法在标准的ImageNet 1000类分类数据集上训练网络160次，使用Darknet神经网络框架，起始学习率为0.1，多项式速率衰减为4次方，权重衰减为0.0005，动量为0.9。在训练过程中，我们使用标准的数据增强技巧，包括随机作物、旋转、色调、饱和度和曝光度的转变。

参数设置：

（1）训练数据集： 标准ImageNet 1000类分类数据集

（2）训练参数： 对网络进行160个epochs的训练，使用初始学习率为0.1随机梯度下降法、4的多项式率衰减法、0.0005的权值衰减法和0.9的动量衰减法

（3）模型： 使用的是Darknet神经网络框架。

（4）数据增强： 在训练中使用标准的数据增强技巧，包括随机的裁剪、旋转、色相、饱和度和曝光变化。

如上所述，在最初的224×224图像训练之后，然后放到448 × 448上微调，但只训练约10个周期。在这个高分辨率下，网络达到很高精度。微调时，10epoch，初始lr0.001。



### 3.3 Training for dectection

检测的训练 我们对这个网络进行了修改，去掉了最后一个卷积层，而是增加了三个3×3的卷积层，每个卷积层有1024个过滤器，然后是最后一个1×1的卷积层，输出的数量是我们检测所需的。对于VOC，我们预测5个框的5个坐标，每个框有20个类别，所以有125个过滤器。我们还从最后的3×3×512层向第二个卷积层添加了一个直通层，以便我们的模型可以使用细粒度的特征。



网络微调：

- 移除最后一个卷积层、global avgpooling层和softmax
- 增加3个3x3x1024的卷积层
- 增加passthrough层
- 增加一个1×1个卷积层作为网络输出层。输出的channel数为num_ anchors×(5+num_ calsses)（num_anchors在文中为5，num _classes=20是类别个数，5是坐标值和置信度）





## 4.Stronger

这章主要是讲联合训练，不太重要



# 三.YOLO v3

参考链接：https://zhuanlan.zhihu.com/p/143747206

https://www.bilibili.com/video/BV1Vg411V7bJ?spm_id_from=333.788.videopod.episodes&vd_source=10d7277f0ba446921a246233fba2160c&p=2

https://jrs0511.blog.csdn.net/article/details/129143961

网络结构图：

![img](C:\Users\14256\Pictures\Screenshots\v2-af7f12ef17655870f1c65b17878525f1_1440w.jpg)

**上图三个蓝色方框内表示Yolov3的三个基本组件**：

1. **CBL：**Yolov3网络结构中的最小组件，由**Conv+Bn+Leaky_relu**激活函数三者组成。
2. **Res unit：**借鉴**Resnet**网络中的残差结构，让网络可以构建的更深。
3. **ResX：**由一个**CBL**和**X**个残差组件构成，是Yolov3中的大组件。每个Res模块前面的CBL都起到下采样的作用，因此经过5次Res模块后，得到的特征图是**608->304->152->76->38->19大小**。

**其他基础操作：**

1. **Concat：**张量拼接，会扩充两个张量的维度，例如26 * 26 * 256和26 * 26 * 512两个张量拼接，结果是26 * 26 * 768。Concat和cfg文件中的route功能一样。
2. **add：**张量相加，张量直接相加，不会扩充维度，例如104*104*128和104*104*128相加，结果还是104*104*128。add和cfg文件中的shortcut功能一样。

**从输入到输出的映射：**

![在这里插入图片描述](C:\Users\14256\Pictures\Screenshots\776e5da02e77b47eedc1d27f61881d39.jpeg)

**yolov3的目标检测损失函数：**

![image-20250721091420603](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250721091420603.png)



## 2.The Deal



### 2.1 Bounding Box Prediction

在YOLOv3的训练中，我们使用了正样本、负样本和忽略样本三种情况，来训练三个框的参数

- 正样本：如果当前预测的包围框比之前其他的任何包围框更好的与ground truth对象重合，那它的置信度就是 1。
- 忽略样本： 如果当前预测的包围框不是最好的，但它和 ground truth对象重合了一定的阈值（这里是0.5）以上，神经网络会忽略这个预测。
- 负样本: 若bounding box 没有与任一ground truth对象对应，那它的置信度就是 0

问题一：

```
Q1：为什么YOLOv3要将正样本confidence score设置为1?

置信度意味着该预测框是或者不是一个真实物体，是一个二分类，所以标签是1、0更加合理。并且在学习小物体时，有很大程度会影响IOU。如果像YOLOv1使用bounding box与ground truth对象的IOU作为confidence，那么confidence score始终很小，无法有效学习，导致检测的Recall不高。
```

问题二：

```
Q2：为什么存在忽略样本?

由于YOLOV3采用了多尺度的特征图进行检测，而不同尺度的特征图之间会有重合检测的部分。例如检测一个物体时，在训练时它被分配到的检测框是第一个特征图的第三个bounding box，IOU为0.98，此时恰好第二个特征图的第一个bounding box与该ground truth对象的IOU为0.95，也检测到了该ground truth对象，如果此时给其confidence score强行打0，网络学习的效果会不理想。
```



### 2.2 Class Prediction(单标签分类改进为多标签分类)

YOLOv3使用的方法：

（1）YOLOv3 使用的是logistic 分类器，而不是之前使用的softmax。

（2）在YOLOv3 的训练中，便使用了Binary Cross Entropy ( BCE, 二元交叉熵) 来进行类别预测。

```
Q：softmax被替代的原因？

（1）softmax只适用于单目标多分类(甚至类别是互斥的假设)，但目标检测任务中可能一个物体有多个标签。(属于多个类并且类别之间有相互关系)，比如Person和Women。
（2）logistic激活函数来完成，这样就能预测每一个类别是or不是。
```



### 2.3 Predictions Across Scales(跨尺度预测)

YOLOv3通过下采样32倍、16倍和8倍得到3个不同尺度的特征图。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/94b189744d0a41ca54ec87020d7528e2.png)



## 3.总结

|              | YOLOv1                                                       | YOLOv2                                                       | YOLOv3                                                       |
| ------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 输入图像尺寸 | 输入的是448×448的三通道图像                                  | 输入的是416×416的三通道图像                                  | 输入的是416×416的三通道图像                                  |
| grid cell    | 每一张图像划分为7×7=49个grid cell                            | 每一张图像划分为13×13=169个grid cell                         | yolov3会产生三个尺度：13×13、26×26、52×52，也对应着grid cell个数。 |
| bbox/anchor  | 每个grid cell 生成2个 bbox（没有anchor），与真实框IOU最大的那个框负责拟合真实框 | 每个grid cell 生成5个anchor框，通过IOU计算选一个anchor产生预测框去拟合真实框 | 每个grid cell生成3个anchor框，通过与gt的IOU计算选一个anchor产生预测框去拟合真实框 |
| 输出张量     | 输出7 * 7 * 30维的张量(30的含义:两组bbox的xywh和置信度+20个类别) | 输出13 * 13 * 125维张量(125的含义：五组anchor的xywh和置信度+20个类别) | 输出三个不同尺寸的张量，但最后都是255，比如S * S * 255，（255含义:三组anchor里xywh+置信度+分类数(COCO数据集80个分类)，所以就是3 * (80+5)。） |
| 预测框数量   | 7 * 7 *2 = 98个预测框                                        | 13 * 13 * 5 = 845个预测框                                    | ( 52 * 52 + 26 * 26 +13 * 13) * 3 = 10647个预测框            |





# 四.YOLOv4

参考链接：https://jrs0511.blog.csdn.net/article/details/129232468

https://jrs0511.blog.csdn.net/article/details/129248856

https://zhuanlan.zhihu.com/p/143747206

https://www.bilibili.com/video/BV1kzDEYdE3i?spm_id_from=333.788.videopod.episodes&vd_source=10d7277f0ba446921a246233fba2160c

YOLOv4网络结构：

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/v2-ccc16892e80035886e36c0100dbd444d_1440w.jpg)

## 0.Abstract

提高CNN准确性的方法：

**（1）专用特性：** 一些特征只针对某一模型，某一问题，或仅为小规模数据集

**（2）通用特性：** 一些特性，如批处理规范化和残差连接，则适用于大多数模型、任务和数据集。这些通用特性包括加权剩余连接(WRC)、跨阶段部分连接(CSP)、跨小批标准化(CmBN)、自反训练(SAT)和Mish 激活函数。

YOLOv4使用的技巧
使用新特性：WRC、CSP、CmBN、SAT、Mish 激活函数、Mosaic数据增强、CmBN、DropBlock正则化、CIoU损失，结合这些技巧实现先进的结果。

## 1.Introduction

贡献
（1）开发了一个高效、强大的目标检测模型。使用单个1080 Ti或2080 Ti GPU就能训练一个超级快速和精确的目标探测器。

（2）验证了在检测器训练过程中，最先进的Bag-of-Freebies 和Bag-of-Specials对目标检测方法的影响。

（3）修改了最先进的方法，使其更有效，更适合于单GPU训练。

问题：

```
Q： Bag-of-Freebies 和Bag-of-Specials

Bag-of-Freebies： 指不会显著影响模型测试速度和模型复杂度的技巧，主要就是数据增强操作、标签软化等外在训练方法，即不需要改变网络模型。
Bag-of-Specials： 是用最新最先进的方法（网络模块）来魔改检测模型。只增加少量推理成本但能显著提高对象检测精度的插件模块和后处理方法，一般来说，这些插件模块都是为了增强模型中的某些属性，如扩大感受野、引入注意力机制或加强特征整合能力等，而后处理是筛选模型预测结果的一种方法。
```

## 2.Related work



### 2.1 Object detection models—目标检测模型

**现代目标检测器组成：**

（1）主干backbone： 在ImageNet上预先训练的网络用来特征提取。

- 在GPU平台上运行的检测器，主干可以是VGG、ResNet、ResNeXt或DenseNet。
- 在CPU平台上运行的检测器，主干可以是SqueezeNet、MobileNet或ShuffleNet。

（2）头部head： 对图像特征进行预测，生成边界框和并预测类别。通常分为两类即单阶段目标检测器和两阶段目标检测器。

- two stage： R-CNN系列，包括fast R-CNN、faster R-CNN、R-FCN和Libra R-CNN。
- one stage： 最具代表性的模型有YOLO、SSD和RetinaNet。

（3）颈部neck： 近年来发展起来的目标检测器常常在主干和头部之间插入一系列混合和组合图像特征的网络层，并将图像特征传递到预测层。称之为目标检测器的颈部neck。

通常，一个颈部neck由几个自下而上的路径和几个自上而下的路径组成。具有该机制的网络包括特征金字塔网络(FPN)、路径汇聚网络(PAN)、BiFPN和NAS-FPN。综上所述，一个普通的物体探测器是由“特征输入、骨干网络、颈部和头部”四部分组成的：

![image-20250721103205808](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250721103205808.png)



### 2.2 Bag of freebies

==BoF方法一：数据增强==

**（1）像素级调整**

- ①光度失真： brightness(亮度)、contrast(对比度)、hue(色度)、saturation(饱和度)、noise(噪声)


- ②几何失真： scaling(缩放尺寸)、cropping(裁剪)、flipping(翻转)、rotating(旋转)


**（2）模拟目标遮挡**

- ①erase(擦除)、CutOut(剪切)： 随机选择图像的矩形区域，并填充随机或互补的零值


- ②hide-and-seek和grid mask： 随机或均匀地选择图像中的多个矩形区域，并将它们替换为全零


- ③将上述方式作用于特征图上： DropOut、DropConnect、DropBlock


**（3）将多张图像组合在一起**

- ①MixUp： 使用两个图像以不同的系数比率相乘后叠加，利用叠加比率调整标签

- ②CutMix： 将裁剪的图像覆盖到其他图像的矩形区域，并根据混合区域大小调整标签


**（4）使用style transfer GAN进行数据扩充，有效减少CNN学习到的纹理偏差。**

==BoF方法二：解决数据集中语义分布偏差问题==

- ①两阶段对象检测器： 使用硬反例挖掘或在线硬例挖掘来解决。不适用于单级目标检测。
- ②单阶段目标检测器： focal损来处理各个类之间存在的数据不平衡问题。

==BoF方法三：边界框(BBox)回归的目标函数==

- ①IoU损失： 将预测BBox区域的区域和真实BBox区域考虑在内。由于IoU是尺度不变的表示，它可以解决传统方法在计算{x, y, w, h}的l1或l2损耗时，损耗会随着尺度的增大而增大的问题。
- ②GIoU loss： 除了覆盖区域外，还包括了物体的形状和方向。他们提出寻找能够同时覆盖预测BBox和地面真实BBox的最小面积BBox，并以此BBox作为分母来代替IoU损失中原来使用的分母。

- ③DIoU loss： 它额外考虑了物体中心的距离。

- ④CIoU loss ： 同时考虑了重叠区域、中心点之间的距离和纵横比。对于BBox回归问题，CIoU具有更好的收敛速度和精度。




### 2.3 Bag of specials

==BoS方法一：插件模块之增强感受野==

**①改进的SPP模块**

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/c2d74d1982506ac86892bed17725b3c3.png)

**②ASPP模块**

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/23e85d47229c155a1fdb75f864fbfc4a.png)

**③RFB模块**

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/72ad2d7bcf6b75c79b04ec9ba747dea2.png)



==BoS方法二：插件模块之注意力机制==

**①channel-wise注意力：** 代表是Squeeze-and-Excitation挤压激励模块(SE)。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/784b9d1e184f867741885a9d06cd5058.png)

**②point-wise注意力：** 代表是Spatial Attention Module空间注意模块(SAM)。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/b2bbeb61de048b0923e593ea5ffc15ed.png)

==BoS方法三：插件模块之特征融合==

**①SFAM：** 主要思想是利用SE模块在多尺度的拼接特征图上进行信道级重加权。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/56c83c1012dc3adeb93492c2c73628f9.png)

**②ASFF：** 使用softmax对多尺度拼接特征图在点维度进行加权。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/797b4d844dd753beec31aa446a64c776.png)

**③BiFPN：** 提出了多输入加权剩余连接来执行按比例的水平重加权，然后添加不同比例的特征图。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/1a822761983ac74f8b68488e54ed9149.png)

==BoS方法四：激活函数==

**①LReLU和PReLU：** 主要目的是解决输出小于0时ReLU的梯度为零的问题。

**②ReLU6和hard-Swish：** 专门为量化网络设计的。

**③SELU：** 针对神经网络的自归一化问题。

**④Swish和Mish：** 都是连续可微的激活函数。

==BoS方法五：后处理==

**①NMS：** 目标检测中常用的后处理方法是NMS, NMS可以对预测较差的bbox进行过滤，只保留响应较高的候选bbox。NMS试图改进的方法与优化目标函数的方法是一致的。NMS提出的原始方法没有考虑上下文信息，所以在R-CNN中加入了分类的置信分作为参考，按照置信分的顺序，从高到低依次进行贪心NMS。

**②soft NMS：** 考虑了对象的遮挡可能导致带IoU分数的贪婪NMS的信心分数下降的问题。

**③DIoU NMS：** 在soft NMS的基础上，将中心点距离信息添加到BBox筛选过程中。值得一提的是，由于以上的后处理方法都没有直接引用捕获的图像特征，因此在后续的无锚方法开发中不再需要后处理。



## 3.Methodology

### 3.1 Selection of architecture

==架构选择目标==

**目标一：在输入网络分辨率、卷积层数、参数数(filter size2×filters × channel / groups)和层输出数(filters)之间找到最优平衡。**

检测器需要满足以下条件：

- ①更高的输入网络大小(分辨率)： 用于检测多个小型对象

- ②更多的层： 一个更高的接受域，以覆盖增加的输入网络的大小

- ③更多的参数： 模型有更强大的能力，以检测单个图像中的多个不同大小的对象。


**目标二：选择额外的块来增加感受野**

不同大小的感受野的影响总结如下：

- ①对象大小： 允许查看整个对象

- ②网络大小： 允许查看对象周围的上下文

- ③超过网络大小： 增加图像点和最终激活之间的连接数


**目标三：选择不同的主干层对不同的检测器层(如FPN、PAN、ASFF、BiFPN)进行参数聚合的最佳方法。**

==YOLOv4架构==

**（1）CSPDarknet53主干（backbone）：** 作者实验对比了CSPResNext50、CSPDarknet53和EfficientNet-B3。从理论与实验角度表明：CSPDarkNet53更适合作为检测模型的Backbone。（还是自家的网络结构好用）

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3e79788a209b9ce3eec42ae82b45460b.png)

```
CSP介绍：
CSP是可以增强CNN学习能力的新型backbone，论文发表2019年11月份
主要技巧：CSPNet将底层的特征映射分为两部分，一部分经过密集块和过渡层，另一部分与传输的特征映射结合到下一阶段。
```

**（2）SPP附加模块增加感受野：** 在CSPDarknet53上添加了SPP块，SPP来源于何恺明大佬的SPP Net因为它显著增加了接受域，分离出了最重要的上下文特性，并且几乎不会降低网络运行速度。

**（3）PANet路径聚合（neck）：** PANet主要是特征融合的改进，使用PANet作为不同检测层的不同主干层的参数聚合方法。而不是YOLOv3中使用的FPN。

**（4）基于锚的YOLOv3头部（head）：** 因为是anchor-base方法，因此分类、回归分支没有改变。

**总结：** YOLOv4模型 = CSPDarkNet53 + SPP + PANet(path-aggregation neck) + YOLOv3-head



### 3.2 Selection of Bof and Bos

为了改进目标检测训练，CNN通常使用以下：

- 激活：ReLU, leaky-ReLU, parametric-ReLU,ReLU6, SELU, Swish, or Mish

- 边界盒回归损失：MSE，IoU、GIoU、CIoU、DIoU
- 数据增强：CutOut, MixUp, CutMix
- 正则化方法：DropOut, DropPath，Spatial DropOut [79], or DropBlock
- 规范化的网络激活（通过均值和方差）：批标准化(BN)[32]，Cross-GPU Batch Normalization(CGBN或SyncBN)[93]，Filter Response Normalization(FRN)[70]，或交叉迭代批标准化(CBN)[89]
- Skip-connections：Residual connections，加权Residual connections、多输入加权Residual connections或Cross stage partial连接(CSP) 

最后的选择：

**（1）激活函数：** 由于PReLU和SELU更难训练，我们选择专门为量化网络设计的ReLU6

**（2）正则化：** 我们选择DropBlock

**（3）归一化：** 由于是单GPU，所以没有考虑syncBN



### 3.3 Additional improvements

==（1）新的数据增强Mosic和自我对抗训练（SAT）==

**①Mosaic：** Mosaic代表了一种新的数据增强方法，它混合了4幅训练图像。基于现有数据极大的丰富了样本的多样性，极大程度降低了模型对于多样性学习的难度。

**②自对抗训练（SAT）：**

- 在第一阶段，神经网络改变原始图像而不是网络权值。通过这种方式，神经网络对自己执行一种对抗性攻击，改变原始图像，以制造图像上没有期望对象的假象。
- 在第二阶段，神经网络以正常的方式对这个修改后的图像进行检测。

==（2）应用遗传算法选择最优超参数==

==（3）修改现有的方法，使设计适合于有效的训练和检测==

**①修改的SAM：** 将SAM从空间上的注意修改为点态注意
![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/68c8c43f6cf22c458aab8160f54cac2c.png)



**②修改PAN：** 将PAN的快捷连接替换为shortcut 连接

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/8819c2fae333f1c148f0d9d5e4e9e49d.png)

**③交叉小批量标准化(CmBN)：** CmBN表示CBN修改后的版本，如图所示，只在单个批内的小批之间收集统计信息。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/5019e806285419cef869af55a6a72176.png)

### 3.4 YOLOv4

==YOLOv4包括==

- 主干(backbone)： CSPDarknet53
- 颈部(neck)： SPP ， PAN
- 头(head)： YOLOv3

==YOLO v4使用==

- Bag of Freebies 外在引入技巧： CutMix和Mosaic数据增强，DropBlock正则化，类标签平滑
- Bag of Specials 网络改进技巧： Mish激活、跨级部分连接(CSP)、多输入加权剩余连接(MiWRC)
- Bag of Freebies 外在检测器引入技巧： CIoU loss, CmBN, DropBlock正则化，Mosaic数据增强，自对抗训练，消除网格敏感性，为一个真值使用多个锚，余弦退火调度，最优超参数，随机训练形状
- Bag of Specials检测器网络改进技巧： Mish激活、SPP-block、SAM-block、PAN路径聚合块、DIoU-NMS



## 4.Experiments

### 4.1 Experimental setup



（1）在ImageNet图像分类实验中，默认超参数为：

-  训练步骤： 8,000,000
-  批大小和小批大小分别： 128和32
-  初始学习率： 0.1
-  warm-up步长： 1000
-  动量衰减： 0.9
-  权重衰减： 0.005

（2）在MS COCO对象检测实验中，默认的超参数为：

-  训练步骤： 500500

-  初始学习率： 0.01
-  warm-up步长： 在400,000步和450,000步分别乘以因子0.1
-  动量衰减： 0.9
-  权重衰减： 0.0005
-  GPU数量： 1个
-  批处理大小： 64



### 4.2 Influence of different features on Classfier training



# YOLOv4结构与方法总结

可以看到由以下四个部分组成：

==输入端：== 训练时对输入端的改进，主要包括Mosaic数据增强、cmBN、SAT自对抗训练

==BackBone主干网络：== 各种方法技巧结合起来，包括：CSPDarknet53、Mish激活函数、Dropblock

==Neck：== 目标检测网络在BackBone和最后的输出层之间往往会插入一些层，比如YOLOv4中的SPP模块、FPN+PAN、SAM结构

==Head：== 输出层的锚框机制和YOLOv3相同，主要改进的是训练时的回归框位置损失函数CIOU Loss，以及预测框筛选的nms变为DIOU nms

YOLOv4的五个基本组件：

- CBM：Yolov4网络结构中的最小组件，由Conv+Bn+Mish激活函数三者组成。
- CBL：由Conv+Bn+Leaky_relu激活函数三者组成。
- Res unit：借鉴Resnet网络中的残差结构，让网络可以构建的更深。
- CSPX：借鉴CSPNet网络结构，由三个卷积层和X个Res unint模块Concate组成。
- SPP：采用1×1，5×5，9×9，13×13的最大池化的方式，进行多尺度融合。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/26252b82c549836b9e328ed26da3e028.png)

## 1.输入端

### 1.1 数据增强

==数据增强①CutMix==

**数据增强的原因：**在平时项目训练时，小目标的AP一般比中目标和大目标低很多。而Coco数据集中也包含大量的小目标，但比较麻烦的是小目标的分布并不均匀。Coco数据集中小目标占比达到41.4%，数量比中目标和大目标都要多。但在所有的训练集图片中，只有52.3%的图片有小目标，而中目标和大目标的分布相对来说更加均匀一些。

**核心思想：**将一部分区域cut掉但不填充0像素，而是随机填充训练集中的其他数据的区域像素值，分类结果按一定的比例分配。

**处理方式：**对一对图片做操作，随机生成一个裁剪框Box，裁剪掉A图的相应位置，然后用B图片相应位置的ROI放到A图中被裁剪的区域形成新的样本，ground truth标签会根据patch的面积按比例进行调整。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/e510741c89c14b601c62edb8a142bd9f.png)

另外两种数据增强的方式：

**（1）Mixup:** 将随机的两张样本按比例混合，分类的结果按比例分配

**（2）Cutout:** 随机的将样本中的部分区域Cut掉，并且填充0像素值，分类的结果不变



==数据增强②Mosaic==

Yolov4中使用的Mosaic是参考2019年底提出的CutMix数据增强的方式，但CutMix只使用了两张图片进行拼接，而Mosaic数据增强则采用了4张图片，随机缩放、随机裁剪、随机排布的方式进行拼接。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/af90279e80242406244d4748ff890644.png)

优点：

**（1）丰富数据集：** 随机使用4张图片，随机缩放，再随机分布进行拼接，大大丰富了检测数据集，特别是随机缩放增加了很多小目标，让网络的鲁棒性更好。

**（2）batch不需要很大：** Mosaic增强训练时，可以直接计算4张图片的数据，使得Mini-batch大小并不需要很大，一个GPU就可以达到比较好的效果。

几种方法的图片解释：

![image-20250729071339619](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729071339619.png)



### 1.2 SAT自对抗训练

自对抗训练(SAT)也代表了一种新的数据增加技术，在两个前后阶段操作。

**（1）在第一阶段：** 神经网络改变原始图像而不是网络权值。通过这种方式，神经网络对自己执行一种对抗性攻击，改变原始图像，以制造图像上没有期望对象的假象。

**（2）在第二阶段：** 神经网络以正常的方式对这个修改后的图像进行检测。

通过引入噪音点进行数据增强


![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/925eb70b952f38e85418694abb591cf7.png)

具体过程：

![image-20250729071849446](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729071849446.png)



### 1.3 CmBN——跨小批量标准化

**BN：** 无论每个batch被分割为多少个mini  batch，其算法就是在每个mini batch前向传播后统计==当前的BN数据==（即每个神经元的期望和方差）并进行Nomalization，BN数据与其他mini batch的数据无关。

**CBN：** 每次iteration中的BN数据是==其之前n次数据和当前数据的和==（对非当前batch统计的数据进行了补偿再参与计算），用该累加值对当前的batch进行Nomalization。好处在于每个batch可以设置较小的size。

**CmBN：** 只在每个Batch内部使用CBN的方法，若每个Batch被分割为一个mini batch，则其效果与BN一致；若分割为多个mini batch，则与CBN类似，只是把mini batch当作batch进行计算，其区别在于权重更新时间点不同，同一个batch内权重参数一样，因此计算不需要进行补偿。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/5eb60c53a74b4a5066c84d331132cb39.png)

### 1.4 Label Smoothing类标签平衡

**原因：**对预测有100%的信心可能表明模型是在记忆数据，而不是在学习。如果训练样本中会出现少量的错误样本，而模型过于相信训练样本，在训练过程中调整参数极力去逼近样本，这就导致了这些错误样本的负面影响变大。

**具体做法：**标签平滑调整预测的目标上限为一个较低的值，比如0.9。它将使用这个值而不是1.0来计算损失。这样就缓解了过度拟合。说白了，这个平滑就是一定程度缩小label中min和max的差距，label平滑可以减小过拟合。所以，适当调整label，让两端的极值往中间凑凑，可以增加泛化性能。

![image-20250729080613292](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729080613292.png)



## 2.主干网络BackBone

### 2.1 CSPDarknet53

**简介：**CSPNet（Cross Stage Partial Networks），也就是跨阶段局部网络。CSPNet解决了其他大型卷积神经网络框架Backbone中网络优化的梯度信息重复问题，CSPNet的主要目的是使网络架构能够实现获取更丰富的梯度融合信息并降低计算量。

**具体做法：**CSPNet实际上是基于Densnet的思想，即首先将数据划分成Part 1和Part 2两部分，Part 2通过dense block发送副本到下一个阶段，接着将两个分支的信息在通道方向进行Concat拼接，最后再通过Transition层进一步融合。CSPNet思想可以和ResNet、ResNeXt和DenseNet结合，目前主流的有CSPResNext50 和CSPDarknet53两种改造Backbone网络。

==ResNeXt网络：==

![image-20250729081339640](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729081339640.png)

==CSPNet网络：==

![image-20250729080757438](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729080757438.png)



```
Q：为什么要采用CSP模块呢？

CSPNet全称是Cross Stage Paritial Network，主要从网络结构设计的角度解决推理中计算量很大的问题。
CSPNet的作者认为推理计算过高的问题是由于网络优化中的梯度信息重复导致的。
因此采用CSP模块先将基础层的特征映射划分为两部分，然后通过跨阶段层次结构将它们合并，在减少了计算量的同时，可以保证准确率。
因此YOLOv4在主干网络Backbone采用CSPDarknet53网络结构，主要有三个方面的有点：
	优点一：增强CNN的学习能力，使得在轻量化的同时保持准确性。
	优点二：降低计算瓶颈
	优点三：降低内存成本
```



### 2.2 Mish激活函数

**简介：**Mish是一个平滑的曲线，平滑的激活函数允许更好的信息深入神经网络，从而得到更好的准确性和泛化；在负值的时候并不是完全截断，允许比较小的负梯度流入。Mish是一个与ReLU和Swish非常相似的激活函数，但是Relu在小于0时完全杀死了梯度，不太符合实际情况，所以可以在不同数据集的许多深度网络中胜过它们。

**公式：**$y=x∗tanh(ln(1+e^x))$

![image-20250729082032161](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729082032161.png)



### 2.3 Dropblock正则化

**传统的Dropout：**随机删除减少神经元的数量，使网络变得更简单。

**Dropblock：**DropBlock技术在称为块的相邻相关区域中丢弃特征。Dropblock方法的引入是为了克服Dropout随机丢弃特征的主要缺点，Dropout主要作用在全连接层，而Dropblock可以作用在任何卷积层之上。这样既可以实现生成更简单模型的目的，又可以在每次训练迭代中引入学习部分网络权值的概念，对权值矩阵进行补偿，从而减少过拟合。

之前的Dropout是随机选择点(b)，现在随机选择一个区域(c)：


![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3d18104ac6c50026c661335bddd18c06.png)



## 3.Neck

### 3.1 SPP

**简介：**SPP-Net全称Spatial Pyramid Pooling Networks，是何恺明大佬提出的，主要是用来解决不同尺寸的特征图如何进入全连接层的，在网络的最后一层concat所有特征图，后面能够继续接CNN模块。

如下图所示，下图中对任意尺寸的特征图直接进行固定尺寸的池化，来得到固定数量的特征。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/365bbfc8b9a7a249857584ac77146b99.png)

具体结构如下：

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/4ecb94892986a1d1be6a051e1d4a888d.png)



### 3.2 PAN

YOLOv3中的neck只有自顶向下的FPN，对特征图进行特征融合，而YOLOv4中则是FPN+PAN的方式对特征进一步的融合。引入了自底向上的路径，使得底层信息更容易传到顶部

下面是YOLOv3的neck中的FPN，如图所示：

FPN是自顶向下的，将高层的特征信息通过上采样的方式进行传递融合，得到进行预测的特征图。


![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/9f2d7b5a1c6ee7da8fc9f7ced6789f93.png)

YOLOv4中的neck如下：

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/2fa0955fea5ebf98ac6be813c93cb551.png)

YOLOv4在原始PAN结构上进行了一点改进，原本的PANet网络的PAN结构中，特征层之间融合时是直接通过addition的方式进行融合的，而Yolov4中则采用在通道方向concat拼接操作融合的，如下图所示。

![img](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/3ef579a909675f006e78393158badfa9.png)



```
Q：为什么要把add改为concat？

add： 将两个特征图直接相加，是resnet中的融合方法，基于这种残差堆叠相加，可以有效地减小因为网络层数加深而导致的cnn网络退化问题。add改变特征图像素值，并没有完全保留原本特征图信息，更多的可以看作对原特征图信息的一种补充，深层特征图在卷积过程中丢失了许多细节信息，通过add的方式得以补全，是在二维的平面上对特征图的增强。因此add在进行图像特征增强时使用最佳。

concat： 将两个特征图在通道数方向叠加在一起，原特征图信息完全保留下来，再对原特征图增加一些我们认为是较好的特征图，丰富了特征图的多样性，是在空间上对原特征图的增强，这样在下一次卷积的过程中我们能得到更好的特征图。
```



### 3.3 SAM



![image-20250729093017771](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729093017771.png)



## 4.Head

### 4.1 损失函数

![image-20250729095913438](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729095913438.png)



### 4.2 IOU

**GIOU：**

![image-20250729100356643](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729100356643.png)

**DIOU：**

![image-20250729100438124](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729100438124.png)

**CIOU：**

![image-20250729100511749](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729100511749.png)





# 五.YOLOv5

YOLOv5模型架构：

![image-20250730085308326](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250730085308326.png)

算法思路：

![image-20250729111751314](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250729111751314.png)





# 六.YOLOv8

参考链接：https://www.bilibili.com/video/BV19nrbYjEyN?spm_id_from=333.788.videopod.episodes&vd_source=10d7277f0ba446921a246233fba2160c



**YOLOv8框架：**

![image-20250731080635352](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250731080635352.png)

v8主干网络参数详解：

![image-20250731084059082](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250731084059082.png)



**C2F模块：**

![image-20250804092817076](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250804092817076.png)



**SPPF模块：**

![image-20250804092910256](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250804092910256.png)

# 七.YOLOv11
