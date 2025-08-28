GoogleColab学一下咋用

# 一.使用过程

打开Anaconda Prompt后按步骤创建即可

## 1.创建conda

选择pytyon=3.10版本号：

![image-20250414170624000](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250414170624000.png)



## 2.安装pytorch

选择12.4的cuda版本的pytorch，网站为：https://pytorch.org/

![image-20250414171018309](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250414171018309.png)



## 3.激活环境后安装ultralytics

![image-20250414172246717](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250414172246717.png)



## 4.安装LabelImg

依次输入下面语句：

```cmd
https://github.com/HumanSignal/labelImg.git
cd labelImg
conda install pyqt=5
conda install -c anaconda lxml
pyrcc5 -o libs/resources.py resources.qrc
python labelImg.py
python labelImg.py [IMAGE_PATH] [PRE-DEFINED CLASS FILE]
```

下次打开时，只需要输入下面语句即可

```cmd
cd labelImg
python labelImg.py
```





## 5.安装roLabelImg

```
cd labelImg
git clone https://gitee.com/wzt9332/roLabelImg.git
cd roLabelImg
pyrcc5 -o resources.py resources.qrc
python roLabelImg.py
```

下次打开时，只需要输入

```python
conda activate roLabelImg_py388
python D:\07.NingBo_Project\2025.04.yolov11_obb\roLabelImg\roLabelImg-master\roLabelImg.py
```



# 二.yolo官方文档阅读

## 1.Quickstart

官方教学文档：https://docs.ultralytics.com/quickstart/#conda-docker-image

### 1.1 Ultralytics的安装

Ultralytics提供了多样的安装方法，**比如pin、conda和Docker**，安装ultralytics时，**需要python>=3.8，Pytorch>=1.8**，使用pip安装语句：

```python
# Install the ultralytics package from PyPI
pip install ultralytics
```

但是在安装Ultralytics前，**需要安装Pytorch环境**。

### 1.2 command-line interface(CLI)

这是一种不需要python环境就可以运行yolo的一种CMD语法，只需要按照CLI的语法在命令行中执行就可以训练，具体使用可参考官方文档：https://docs.ultralytics.com/usage/cli/

**训练例子：**

```cmd
yolo train data=coco8.yaml model=yolo11n.pt epochs=10 lr0=0.01
```

### 1.3 在python环境下使用Ultralytics

可以使用python完成Ultalytics的应用，具体的使用可参考官方文档：https://docs.ultralytics.com/usage/python/

**例子如下：**

```python
from ultralytics import YOLO

# Create a new YOLO model from scratch
model = YOLO("yolo11n.yaml")

# Load a pretrained YOLO model (recommended for training)
model = YOLO("yolo11n.pt")

# Train the model using the 'coco8.yaml' dataset for 3 epochs
results = model.train(data="coco8.yaml", epochs=3)

# Evaluate the model's performance on the validation set
results = model.val()

# Perform object detection on an image using the model
results = model("https://ultralytics.com/images/bus.jpg")

# Export the model to ONNX format
success = model.export(format="onnx")
```



### 1.4 Ultralytics参数

可以使用python语法看现在的设置状况，通过修改默认值可更改性能，具体使用参考官方文档：https://docs.ultralytics.com/usage/cfg/

**查看参数：**

```python
from ultralytics import settings

# View all settings
print(settings)

# Return a specific setting
value = settings["runs_dir"]
```

**修改参数：**

```python
from ultralytics import settings

# Update a setting
settings.update({"runs_dir": "/path/to/runs"})

# Update multiple settings
settings.update({"runs_dir": "/path/to/runs", "tensorboard": False})

# Reset settings to default values
settings.reset()
```



## 2.Python环境下使用Ultralytics

在python环境下，使用者可以加载一个模型、训练它、在验证集上评估它的表现并用ONNX的格式输出模型参数

**例子如下：**

==首先从头创建一个yolo模型-->加载一个与训练好的模型-->使用数据集训练模型-->使用验证机评估模型-->使用训练好的模型进行实际预测-->将模型参数输出问ONNX格式，以便传递给他人重复利用==

```python
from ultralytics import YOLO

# Create a new YOLO model from scratch
model = YOLO("yolo11n.yaml")

# Load a pretrained YOLO model (recommended for training)
model = YOLO("yolo11n.pt")

# Train the model using the 'coco8.yaml' dataset for 3 epochs
results = model.train(data="coco8.yaml", epochs=3)

# Evaluate the model's performance on the validation set
results = model.val()

# Perform object detection on an image using the model
results = model("https://ultralytics.com/images/bus.jpg")

# Export the model to ONNX format
success = model.export(format="onnx")
```



### 2.1 Train(训练)

使用定制的数据集来进行模型的训练，模型使用特制的数据集和超参数训练，训练过程包括了优化模型的参数，以便它能够准确的预测类别和准求定位出图片中物体的位置，参考文档：https://docs.ultralytics.com/modes/train/

**预训练：**

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")  # pass any model type
results = model.train(epochs=5)
```

**从头开始训练：**

```python
from ultralytics import YOLO

model = YOLO("yolo11n.yaml")
results = model.train(data="coco8.yaml", epochs=5)
```

**重新开始训练：**

```python
model = YOLO("last.pt")
results = model.train(resume=True)
```

像COCO、VOC、ImageNet和其它许多数据集已经自动的被下载到了**yolo train data=coco.yaml**里面



#### 2.1.1 yolov11训练模型的关键特点

**1.自动的数据集下载：**像COVO、VOC和ImageNet这样的标准数据集已经被自动的下载

**2.多GPU的支持：**可以使用多张GPU进行训练

**3.超参数的构造：**可以通过更感YAML configuration文件进行超参数的改进

**4.可视化和监督：**训练矩阵的实时追踪和更好观察学习过程的可视化



#### 2.1.2 训练过程的例子

YOLO11n在COCO8数据集上使用640张图片，循环迭代一百次，训练设备可以使用device语句指定为特殊设备，如果没有内容，那么divice将被设置为0，下面的例子说明了如何训练：

**1。单张GPU或CPU训练例子：**

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.yaml")  # build a new model from YAML
model = YOLO("yolo11n.pt")  # load a pretrained model (recommended for training)
model = YOLO("yolo11n.yaml").load("yolo11n.pt")  # build from YAML and transfer weights

# Train the model
results = model.train(data="coco8.yaml", epochs=100, imgsz=640)
```



**2。多张GPU训练例子：**

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # load a pretrained model (recommended for training)

# Train the model with 2 GPUs
results = model.train(data="coco8.yaml", epochs=100, imgsz=640, device=[0, 1])
```



**3.MAC上训练例子：**

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # load a pretrained model (recommended for training)

# Train the model with MPS
results = model.train(data="coco8.yaml", epochs=100, imgsz=640, device="mps")
```



#### 2.1.3 重新训练被打断的上一个模型

当训练被重新开始后，Ultralytics YOLO从上一个被保留的模型中加载权重，并且也存储了如优化器、学习率和迭代次数这种参数，这允许了我们可以无缝衔接上一次的训练过程，我们使用resume=True、并将路径改为上次的.pt开始重新训练

**重新训练例子：**

```python
from ultralytics import YOLO

# Load a model
model = YOLO("path/to/last.pt")  # load a partially trained model

# Resume training
results = model.train(resume=True)
```

通过将resume设置为True，train函数将继续从上一次退出的地方进行训练，并存储在 'path/to/last.pt'文件中



#### 2.1.4 训练参数

YOLO模型包含了各种各样的训练超参数，这些参数影响着模型的表现、速度和准确性。关键的训练参数有：**batch_size, learning rate, momentum, and weight decay**，另外，**优化器、损失函数、训练数据集的组成**也能影响训练过程。

Batch-size参数可以大致设置为以下三种方式：

- **Fixed [Batch Size](https://www.ultralytics.com/glossary/batch-size)**: 设置一个整数 (e.g., `batch=16`), 直接指定每次读取图片的数量
- **Auto Mode (60% GPU Memory)**: 使用 `batch=-1` 去自动的调整大约 60% CUDA 内存利用.
- **Auto Mode with Utilization Fraction**: 设置 (e.g., `batch=0.70`) 去指定GPU内存分数的使用大小



#### 2.1.5 增强设置和超参数

增强技术对于增强模型的鲁棒性和表现是必要的，可以帮助模型更好的生成哪些看不见的数据



#### 2.1.6 Logging(日志)

通过日志，我们可以持续查看模型在过去的表现，YOLO提供了三种类型的日志，Comet、ClearML和TensorBoard，具体怎么用这章还没看，暂时用不到



### 2.2 Val(验证)

验证模型是用来验证训练后的模型性能，模型在验证集上被评估它的准确性和一般表现，参考文档：https://docs.ultralytics.com/modes/val/

**在训练后评估：**

```python
from ultralytics import YOLO

# Load a YOLO model
model = YOLO("yolo11n.yaml")

# Train the model
model.train(data="coco8.yaml", epochs=5)

# Validate on training data
model.val()
```

**在另一个数据集上评估：**

```python
from ultralytics import YOLO

# Load a YOLO model
model = YOLO("yolo11n.yaml")

# Train the model
model.train(data="coco8.yaml", epochs=5)

# Validate on separate data
model.val(data="path/to/separate/data.yaml")
```



#### 2.2.1yolov11验证模型的关键特点

**1.自动设置：**模型记得训练构造以便直接验证

**2.支持多个评估标准：**可以基于一系列的准确率度量准则来预测模型性能

**3.CLI和Python的API调用：**可以使用CLI和Python来验证模型的表现

**4.数据通用性：**可以与训练阶段的模型数据进行无缝衔接



YOLO11模型自动的记住了他们的训练设置，所以我们可以在相同的图片尺寸上验证一个模型



#### 2.2.4 验证过程的例子

在COCO8数据集上验证一个已经训练好的YOLO11n模型，没有参数是需要的，因为model包含了它的训练数据和参数作为模型属性

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # load an official model
model = YOLO("path/to/best.pt")  # load a custom model

# Validate the model
metrics = model.val()  # no arguments needed, dataset and settings remembered
metrics.box.map  # map50-95
metrics.box.map50  # map50
metrics.box.map75  # map75
metrics.box.maps  # a list contains map50-95 of each category
```



#### 2.2.3 验证参数

使用参数的例子：

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")

# Customize validation settings
validation_results = model.val(data="coco8.yaml", imgsz=640, batch=16, conf=0.25, iou=0.6, device="0")
```



#### 2.2.4 使用定制数据集来验证

代码如下：

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")

# Validate with a custom dataset
metrics = model.val(data="path/to/your/custom_dataset.yaml")
print(metrics.box.map)  # map50-95
```



#### 2.2.5 将验证结果保存为JSON文件

代码如下：

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")

# Save validation results to JSON
metrics = model.val(save_json=True)
```





### 2.3 Predict(预测)

预测模型是用来做预测的，使用一个在新的图像或视频上训练的YOLO模型，在这个节点中，模型被加载到了一个checkpoint文件，使用者可以提供图像或者视频去执行推断。下面的例子，模型预测了被输入的图像或视频中，物体的类别和位置。参考链接：https://docs.ultralytics.com/modes/predict/#inference-sources

下面代码展示了YOLO模型的多张输入方式以及预测结果的保存方式：

- 输入支持:
  - 视频流(如摄像头)
  - 图像文件夹
  - 单张图像(PIL或Numpy数组)
  - 图像列表(多个PIL或Numpy图像)
- 输出支持：
  - 显示预测结果
  - 保存预测图像
  - 保存预测结果为文本文件

```python
import cv2
from PIL import Image

from ultralytics import YOLO

model = YOLO("model.pt")
# accepts all formats - image/dir/Path/URL/video/PIL/ndarray. 0 for webcam
results = model.predict(source="0")	# 参数为0表示从默认网络摄像头捕获视频流
results = model.predict(source="folder", show=True)  # 从文件夹中读取数据，在预测时显示图像及其检测结果

# from PIL
im1 = Image.open("bus.jpg")	# 使用PIL读取图像，保存为一个PIL图像对象
results = model.predict(source=im1, save=True)  # 将预测结果保存为新图像(带有绘制的边界框、标签等)

# from ndarray
im2 = cv2.imread("bus.jpg")	# 使用OpenCV加载图像，并保存为一个Numpy数组
results = model.predict(source=im2, save=True, save_txt=True)  # 将预测结果保存为文本文件

# from list of PIL/ndarray
results = model.predict(source=[im1, im2])	# 使用YOLO模型对图像列表进行批量预测
```

但是默认的存储方式或造成内存爆炸，以下是解决办法：

```python
# results would be a list of Results object including all the predictions by default
# but be careful as it could occupy a lot memory when there're many images,
# especially the task is segmentation.

# 1. return as a list
results = model.predict(source="folder")
# 默认情况下，results 是一个包含所有预测结果的 list，其中每个元素都是一个 Results 对象。

# 2. return as a generator
results = model.predict(source=0, stream=True) 
# 设置 stream=True，YOLO 模型将返回一个 生成器（generator）而不是列表。

# 遍历生成器并提取预测结果
for result in results:
    # Detection
    result.boxes.xyxy  # 边界框坐标，格式为 xyxy，形状为 (N, 4)
    result.boxes.xywh  # 边界框坐标，格式为 xywh（中心点+宽高），形状为 (N, 4)
    result.boxes.xyxyn  # 归一化的 xyxy 格式坐标，形状为 (N, 4)
    result.boxes.xywhn  # 归一化的 xywh 格式坐标，形状为 (N, 4)
    result.boxes.conf  # 置信度分数，形状为 (N, 1)
    result.boxes.cls  # 分类标签，形状为 (N, 1)

    # Segmentation
    result.masks.data  # 分割掩码数据，形状为 (N, H, W)
    result.masks.xy  # 每个分割区域的像素点坐标，类型为 List[segment] * N
    result.masks.xyn  # 归一化的分割区域像素点坐标，类型为 List[segment] * N

    # Classification
    result.probs  # 分类概率分布，形状为 (num_class, )

# Each result is composed of torch.Tensor by default,
# in which you can easily use following functionality:
result = result.cuda() # 将 result 的所有张量（torch.Tensor）移动到 GPU 上。
result = result.cpu()	# 将 result 的所有张量移动到 CPU 上
result = result.to("cpu") # 等同于 result.cpu()，显式指定将张量移动到 CPU。
result = result.numpy()	# 将张量转换为 NumPy 数组，方便与 NumPy 库进行操作。
```



#### 2.3.1 预测节点的关键特点

**1.支持多数据格式：**可查看官方文档查看支持的数据格式

**2.Streaming模式：**使用stream可以使用生成器来保存预测结果，以防内存爆炸

**3.批量处理：**在处理多图像和视频的能力大幅提升

**4.友好的一体化：**可以和其它的软件组成和数据流进行融合

使用stream=False返回一个list：

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # pretrained YOLO11n model

# Run batched inference on a list of images
results = model(["image1.jpg", "image2.jpg"])  # return a list of Results objects

# Process results list
for result in results:
    boxes = result.boxes  # Boxes object for bounding box outputs
    masks = result.masks  # Masks object for segmentation masks outputs
    keypoints = result.keypoints  # Keypoints object for pose outputs
    probs = result.probs  # Probs object for classification outputs
    obb = result.obb  # Oriented boxes object for OBB outputs
    result.show()  # display to screen
    result.save(filename="result.jpg")  # save to disk
```

使用stream=True返回一个generator：

```python
from ultralytics import YOLO

# Load a model
model = YOLO("yolo11n.pt")  # pretrained YOLO11n model

# Run batched inference on a list of images
results = model(["image1.jpg", "image2.jpg"], stream=True)  # return a generator of Results objects

# Process results generator
for result in results:
    boxes = result.boxes  # Boxes object for bounding box outputs
    masks = result.masks  # Masks object for segmentation masks outputs
    keypoints = result.keypoints  # Keypoints object for pose outputs
    probs = result.probs  # Probs object for classification outputs
    obb = result.obb  # Oriented boxes object for OBB outputs
    result.show()  # display to screen
    result.save(filename="result.jpg")  # save to disk
```



#### 2.3.2 输入源类型

YOLO11可以处理不同的输入源来进行推断，具体的可以使用的输入源可参考官方文档

```python
from ultralytics import YOLO

# Load a pretrained YOLO11n model
model = YOLO("yolo11n.pt")

# Define path to the image file
source = "path/to/image.jpg"

# Run inference on the source
results = model(source)  # list of Results objects
```



#### 2.3.3 推断参数

model.predict()应用了多个参数

```python
from ultralytics import YOLO

# Load a pretrained YOLO11n model
model = YOLO("yolo11n.pt")

# Run inference on 'bus.jpg' with arguments
model.predict("https://ultralytics.com/images/bus.jpg", save=True, imgsz=320, conf=0.5)
```



### 2.4 Export(输出)

输出模式是用来输出一个YOLO模型，到一个可以被应用的格式，在这个模式中，模型被转化为一个格式，这个格式可以被其他的软件和硬件所使用，这个模式是有用的当部署模型到生成环境时

**输出一个官方的YOLO模型到ONNX格式，使用动态的批量大小和图像大小：**

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")
model.export(format="onnx", dynamic=True)
```

**输出一个官方的YOLO模型到TensorRT格式，设置device=0为了CUDA设备的加速：**

```python
from ultralytics import YOLO

model = YOLO("yolo11n.pt")
model.export(format="engine", device=0)
```



### 2.5 Track(回溯)



### 2.6 Benchmark(基准)



### 2.7 Using Trainers(使用训练器)



## 3.Configuration(构造模块)

YOLO设置和超参数在模型的表现、速度和准确性方面扮演了一个重要的角色，这些设置能够影像模型的表现，在各种各样的阶段，包括训练、验证和预测，具体参数设置参考官方文档：https://docs.ultralytics.com/usage/cfg/#how-do-i-improve-my-yolo-models-performance-during-training

YOLO 的 **Configuration 模块** 提供了一种灵活的机制，用于管理和自定义模型的训练、验证和推理时的各种参数和配置。它的主要作用是：

1. **集中管理参数**：
   - 将训练/验证/推理所需的参数和超参数集中在一个配置文件中，便于修改和复用。
   - 例如，学习率、优化器类型、冻结层数、数据增强方法等。
2. **提高可读性**：
   - 使用配置文件而不是硬编码参数，可以让代码更加简洁、清晰。
   - 配置文件通常是 YAML 格式，具有更好的可读性和结构化。
3. **自定义实验配置**：
   - 通过配置文件，可以快速调整实验参数并进行不同实验的对比。
   - 不需要修改代码，只需切换配置文件即可改变训练或推理的行为。
4. **支持不同任务**：
   - YOLO 支持多任务（目标检测、分割、分类），配置文件可以帮助快速调整任务相关的参数（如损失函数、数据集类别等）。

以下是 YOLO 配置文件中常见的参数分类及其作用：

| 参数类别       | 参数名称      | 作用                                           |
| -------------- | ------------- | ---------------------------------------------- |
| **基础设置**   | `epochs`      | 训练的 epoch 数量。                            |
|                | `batch`       | 每个训练批次的样本数量。                       |
|                | `data`        | 数据集的路径或配置文件（如 `coco128.yaml`）。  |
|                | `imgsz`       | 输入图像的大小（例如 640x640）。               |
|                | `device`      | 设置训练设备（如 `cpu` 或 `cuda:0`）。         |
| **优化器设置** | `lr0`         | 初始学习率。                                   |
|                | `optimizer`   | 优化器类型（如 `SGD` 或 `Adam`）。             |
| **模型设置**   | `model`       | 模型权重文件路径（如 `yolov8n.pt`）。          |
|                | `pretrained`  | 是否使用预训练权重。                           |
|                | `freeze`      | 冻结模型的前几层（如主干网络）。               |
| **数据增强**   | `augment`     | 是否启用数据增强。                             |
|                | `mosaic`      | 是否使用 Mosaic 数据增强。                     |
| **日志和监控** | `project`     | 保存结果的项目名称。                           |
|                | `name`        | 保存结果的运行名称。                           |
|                | `save_period` | 每隔多少 epoch 保存一次模型权重。              |
| **任务相关**   | `task`        | 任务类型（如 `detect`/`segment`/`classify`）。 |
|                | `nc`          | 数据集的类别数量（如 COCO 数据集有 80 类）。   |

使用配置文件进行训练：

示例配置文件train_config.yaml:

```yaml
# train_config.yaml

# 训练设置
epochs: 50
batch: 16
imgsz: 640

# 模型设置
model: yolov8n.pt  # 使用 YOLOv8n 的预训练模型
pretrained: true   # 启用预训练
freeze: [0, 10]    # 冻结前 10 层

# 优化器设置
lr0: 0.01          # 初始学习率
optimizer: Adam    # 使用 Adam 优化器

# 数据集设置
data: coco128.yaml # 数据集配置文件
task: detect       # 任务是目标检测
nc: 80             # 类别数量

# 日志与保存
project: yolov8_experiments
name: run1
save_period: 5     # 每隔 5 个 epoch 保存一次权重
```

启动训练：

```python
from ultralytics import YOLO

# 加载 YOLO 模型
model = YOLO("yolov8n.pt")

# 使用配置文件启动训练
model.train(cfg="train_config.yaml")
```



## 4.Simple Utilities(简单实用工具)

Ultralytics YOLO提供了一些简单的实用工具，这些工具用于支持、优化和加速机器学习工作流，它们涵盖了数据处理、注释生成、格式转换、可视化、数据增强等多个方面，官方参考文档：https://docs.ultralytics.com/usage/simple-utilities/



### 4.1 数据工具

####  4.1.1 Auto Labeling / Annotations(自动标注)

使用Ultralytics YOLO预训练模型结合SAM(Segment Anything Model)对新数据进行自动标注，生成分割格式的数据

**示例代码：**

```python
from ultralytics.data.annotator import auto_annotate

auto_annotate(
    data="path/to/new/data",
    det_model="yolo11n.pt",
    sam_model="mobile_sam.pt",
    device="cuda",
    output_dir="path/to/save_labels",
)
```



#### 4.1.2 Visualize Dataset Annotations(可视化数据集标注)

这个函数可在训练前可视化YOLO标注，帮助检测数据标注的正确性，如边界框、类别标签等

**示例代码：**

```python
from ultralytics.data.utils import visualize_image_annotations

label_map = {  # Define the label map with all annotated class labels.
    0: "person",
    1: "car",
}

# Visualize
visualize_image_annotations(
    "path/to/image.jpg",  # Input image path.
    "path/to/annotations.txt",  # Annotation file path for the image.
    label_map,
)
```



#### 4.1.3 Convert Segmentation Masks into YOLO Format(分割掩码转换为YOLO格式)



## 5.Adcanced Customization(先进定制)

主要讲了一下如何修改代码，根据自己的任务定制化代码

















# Q&A

1.检测用的什么算法

**halcon算法，没用yolo**

2.指标是什么

3.有哪几种缺陷

**主要还是二分类，还没有多标签，因为缺陷种类很多**

4.对模型的大小、推理速度的要求

5.检测的工作流程

6.目前的需求

**完全代替人工**

7.下一步：

**diffusion、GAN生成对抗**























