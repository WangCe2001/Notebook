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





# 借鉴方向

YOLOv11：C3k2与C2PSA模块

### 2.2 核心组件深度剖析

#### 2.2.1 C3k2模块：动态感受野的基石

YOLOv11引入了**C3k2模块**来替代YOLOv8中的C2f模块 。C3k2不仅继承了CSP（Cross Stage Partial）网络的梯度流分流思想，还引入了可定制的卷积核机制。  

- **机制原理**：C3k2允许网络在不同的深度动态选择卷积核大小。在PCB检测中，大的卷积核有助于捕捉宏观结构（如元件布局），而小的卷积核则专注于微观纹理（如焊盘表面的裂纹）。
- **对PCB检测的意义**：PCB缺陷往往尺度跨度极大，从占据半个图像的“缺损”到仅有几个像素的“针孔”。C3k2的跨尺度特征提取能力使其能够更好地适应这种尺度变化，减少了对固定锚框的依赖。

#### 2.2.2 C2PSA模块：空间注意力的强化

另一个关键创新是**C2PSA（Cross Stage Partial with Spatial Attention）**模块 。  

- **机制原理**：该模块在特征融合阶段引入了空间注意力机制。它不仅关注“是什么”（通道注意力），更关注“在哪里”（空间注意力）。
- **对PCB检测的意义**：PCB图像通常包含大量复杂的背景纹理（如丝印字符、玻纤纹理），这些都是干扰项。C2PSA能够抑制这些背景噪声的权重，迫使模型聚焦于具有缺陷特征的区域（如线路边缘的突起或凹陷）。这对于降低误报率（False Positive Rate）具有决定性作用。

#### 2.2.3 解耦检测头（Decoupled Head）

YOLOv11延续并优化了解耦检测头的设计，将分类（Classification）和回归（Regression）任务分离 。  

- **机制原理**：分类任务关注纹理语义，回归任务关注边缘几何。两者在特征空间上的分布是不一致的。解耦头通过不同的分支分别处理，避免了任务冲突。
- **对PCB检测的意义**：PCB缺陷的类别往往与其位置强相关（例如，“连锡”只能发生在两个焊盘之间）。解耦头允许模型更精确地学习这些几何约束，从而提升定位精度（IoU）。



**YOLOv11的独特优势**： 根据Ultralytics官方及相关技术分析，YOLOv11在架构上进行了多项针对性改进，使其特别适合精密工业检测：  

1. **C3k2模块**：作为Backbone的核心组件，C3k2替代了YOLOv8的C2f。它通过引入自定义内核大小的卷积，在保持感受野的同时减少了参数冗余，是一种更高效的跨阶段局部网络实现。这使得模型在提取PCB复杂纹理特征时更加高效。  
2. **C2PSA注意力机制**：在SPPF模块后引入了C2PSA（Cross Stage Partial with Spatial Attention）。该模块融合了多头自注意力机制（Self-Attention），能够增强模型对空间信息的全局感知能力。对于PCB上分布稀疏且细小的缺陷，C2PSA有助于模型聚焦于关键区域，抑制背景噪声。  
3. **多尺度与参数效率**：YOLOv11m在参数量比YOLOv8m减少22%的情况下，实现了更高的COCO mAP。这意味着在同等算力下，YOLOv11能部署更深的网络，或者在同等精度下拥有更快的推理速度（FPS）。  



# 自定义方向

常见的PCB表面缺陷包括：**缺孔（Missing Hole）、鼠咬（Mouse Bite）、开路（Open Circuit）、短路（Short Circuit）、毛刺（Spur）以及余铜（Spurious Copper）**。

1.样本稀疏性问题：

公开数据集：DeepPCB和PKU-Market-PCB

GAN生成+Diffusion扩散模型，Stable diffusion+controlNet技术



2.网络结构：

引入注意力机制（SE, CBAM, ECA）以增强特征提取能力 

利用多尺度特征融合（FPN, PANet）来解决尺寸变化问题 

以及改进损失函数（如CIoU, SIoU）以提升定位精度



P2检测头、BiFPN(Bidirectional Feature Pyramid Netword)特征融合、WIou(Sise-IOU)损失函数、NWDLoss(Normalized Wasserstein Distance)函数、EMA(Efficient Multi-Scale Attention、swim transformer、CBAM&SimAM(convolutional Block Attention Module)、PCB-DETR(Detection Transformer)、(Spatial Attention Offest Module)、SPD-Conv与StarNet、SimAM模块



3.模型轻量化：

利用**LAMP（Layer Adaptive Magnitude-based Pruning）** 策略，根据权重幅值对模型进行通道剪枝，剔除冗余通道，力争在精度损失<1%的前提下减少30%的参数量 。



技术栈确立：

1.数据层：针对样本稀疏，使用stable Diffusion + ControlNEt生成缺陷数据



2.算法层：针对小目标与形变，改进YOLOv11，组合策略：SPD-Conv+BiFPN+NWD Loss

Neck端：引入BiFPN或AFPN，替换原有的PANet，增强特征融合

Head端：增加一个P2检测头

Loss端：使用NWD或WIou Loss函数

Attention：在Backbone末端加一个SimAM





# 参考规划：

参考链接：

https://gemini.google.com/share/204fd15b5a09

## 4. 研究路线建议：基于YOLOv11的改进策略

针对上述痛点，结合YOLOv11的特性，本节为您详细规划了毕业论文的研究路线。建议将研究分为数据增强、架构改进、损失函数优化和工程部署四个阶段。

### 4.1 第一阶段：数据工程与生成式AI增强

数据是深度学习的天花板。鉴于PCB缺陷数据的稀缺性，建议引入生成式AI技术进行数据合成，这是一个非常前沿且容易出彩的研究点。

#### 4.1.1 基础数据集准备

- **DeepPCB数据集**：包含1500对图像（模板图与测试图），涵盖6类缺陷（Open, Short, Mouse bite, Spur, Pin hole, Spurious copper）。作为基准数据集。  
- **PKU-Market-PCB数据集**：包含约1386张合成图像，具有旋转和光照变化，用于测试泛化性 。  

#### 4.1.2 生成式数据增强（Generative Data Augmentation）

除了传统的Mosaic（马赛克）和Mixup增强外，建议探索以下前沿方法 ：  

- **Stable Diffusion + ControlNet + LoRA**：
  - **原理**：利用Stable Diffusion强大的图像生成能力，配合ControlNet（如Canny或Depth模式）锁定PCB的线路结构，防止生成变形的电路。
  - **实施**：训练一个针对PCB纹理的LoRA（Low-Rank Adaptation）模型，微调底模。然后使用Inpainting（重绘）技术，在良品PCB的特定区域“画”出缺陷。例如，在两条线路之间mask一个区域，Prompt提示生成“solder bridge”或“short circuit”。
  - **优势**：这种方法生成的缺陷融合度极高，光影效果自然，远优于简单的“贴图”合成，能有效提升模型对罕见缺陷的识别能力 。  
- **GAN（生成对抗网络）**：虽然逐渐被Diffusion取代，但CycleGAN在风格迁移（如将不同颜色的PCB互转）方面仍有应用价值，可用于扩充背景多样性 。  

### 4.2 第二阶段：YOLOv11架构的针对性改进

这是论文的核心创新点部分。建议从以下三个维度对原生YOLOv11进行手术式改造。

#### 4.2.1 引入P2微小目标检测头

- **问题**：YOLOv11默认输出P3, P4, P5三个尺度的特征图，最小Stride为8。对于微小缺陷，信息丢失严重。
- **改进方案**：增加一个**P2检测头**（Stride=4）。从Backbone的较浅层（高分辨率层）引出特征，经过C3k2模块处理后，与Neck层进行融合 。  
- **预期效果**：这将显著提升针孔（Pin hole）和微小划痕的Recall（召回率），虽然会增加一定的计算量，但对于PCB质检是值得的权衡。

#### 4.2.2 特征融合网络的升级：BiFPN

- **问题**：原生PANet简单地将不同尺度的特征相加或拼接，忽略了不同尺度特征的重要性差异。
- **改进方案**：引入**BiFPN（Bidirectional Feature Pyramid Network）**。BiFPN使用加权特征融合，赋予重要的特征层更高的权重，并增加了跨尺度的跳跃连接 。  
- **实施**：修改`yolo11.yaml`，将Concat操作替换为加权融合节点。这将帮助模型在深层语义和浅层纹理之间找到最佳平衡点。

#### 4.2.3 嵌入特定注意力机制

- **改进方案**：在Backbone的末端或Neck的关键节点嵌入**EMA（Efficient Multi-Scale Attention）\**或\**CBAM（Convolutional Block Attention Module）** 。  
- **理由**：CBAM结合了通道注意力和空间注意力，能有效抑制PCB丝印文字等背景噪声。EMA则在不增加太多计算量的前提下，增强了多尺度特征的表达能力，非常适合处理尺寸多变的缺陷。

### 4.3 第三阶段：损失函数与训练策略优化

#### 4.3.1 引入WIoU（Wise-IoU）损失函数

- **背景**：YOLOv11默认使用CIoU。但在PCB数据集中，存在许多低质量标注或边界模糊的缺陷。CIoU会强行惩罚这些样本，可能导致模型震荡。
- **改进**：采用**WIoU v3**。WIoU引入了动态非单调聚焦机制（Dynamic Non-Monotonic Focusing），它能智能地减少对“极端困难样本”（可能是标注错误）的关注，同时提升普通困难样本的权重 。  
- **预期效果**：加快收敛速度，并提升最终的mAP@0.5:0.95指标。

#### 4.3.2 Inner-IoU辅助边界框回归

- **改进**：引入**Inner-IoU**或**Inner-MPDIoU**。通过引入辅助框（Auxiliary Bounding Box）来计算IoU损耗，可以加速微小目标的回归收敛 。这对于PCB上的细长型缺陷（如开路、短路）特别有效。  

### 4.4 第四阶段：边缘部署与工程落地

为了体现研究的应用价值，必须验证模型在实际工业硬件上的表现。

#### 4.4.1 硬件平台选择

建议选用**NVIDIA Jetson Orin Nano**或**Jetson Orin NX**。这是目前工业界最主流的边缘AI计算平台，Ultralytics官方对Jetson有良好的支持 。  

#### 4.4.2 TensorRT推理加速

- **实施**：将训练好的PyTorch模型（.pt）导出为ONNX格式，再使用TensorRT将其编译为Engine文件（.engine）。
- **数据支撑**：根据基准测试，YOLOv11n在Jetson Orin Nano上使用TensorRT（FP16精度）的推理耗时约为4.91ms（>200 FPS），而直接使用PyTorch则需21.3ms 。这种加速比是论文中展示工程能力的关键数据。  

#### 4.4.3 量化感知训练（QAT）

- **挑战**：直接将模型量化为INT8（8位整数）虽然速度最快，但对于PCB微小缺陷，精度损失（Accuracy Drop）可能无法接受 。  
- **解决方案**：采用**量化感知训练（Quantization-Aware Training, QAT）**。在训练过程中模拟量化噪声，让模型“适应”低精度表示，从而在保持INT8速度的同时，将精度损失降到最低 。  

------

## 5. 实验设计与评估指标体系

在开题报告中，必须清晰地定义如何评价你的模型。

### 5.1 评价指标（Metrics）

不能仅看mAP，必须建立多维度的评价体系：

- **mAP@0.5**：衡量检测能力的基准指标。
- **mAP@0.5:0.95**：衡量高精度定位能力的指标（PCB检测要求框得很准）。
- **Recall（召回率）**：**最关键的工业指标**。必须单独列出各类缺陷的Recall，因为漏检（False Negative）是工业质检的底线 。  
- **FPS（帧率）与 Latency（延迟）**：在Jetson平台上的实测数据，证明实时性。
- **GFLOPs与参数量**：证明模型的轻量化程度。

### 5.2 消融实验（Ablation Study）设计

为了证明你的改进有效，需要设计严谨的对比实验 ：  

| 实验组   | 基础模型 | 改进点1 (P2头) | 改进点2 (BiFPN) | 改进点3 (WIoU) | mAP@0.5   | Recall    | 推理耗时 (ms) |
| -------- | -------- | -------------- | --------------- | -------------- | --------- | --------- | ------------- |
| Baseline | YOLOv11n | ×              | ×               | ×              | 92.5%     | 88.1%     | 5.2           |
| Exp 1    | YOLOv11n | √              | ×               | ×              | 94.1%     | 91.2%     | 6.5           |
| Exp 2    | YOLOv11n | √              | √               | ×              | 95.3%     | 92.8%     | 7.1           |
| Exp 3    | YOLOv11n | √              | √               | √              | **96.8%** | **94.5%** | 7.1           |

*注：以上数据为预期假设，实际论文中需填入实验结果。*

### 5.3 对比实验

将改进后的模型与当前主流模型进行对比：

- **Anchor-Based**: YOLOv5, YOLOv7
- **Anchor-Free**: YOLOv8, YOLOv10
- **Transformer**: RT-DETR (证明CNN在小目标和速度上的优势)  

------

## 6. 结论与展望

### 6.1 预期贡献

本研究预计将在以下几个方面做出贡献：

1. **理论层面**：揭示YOLOv11架构在微小瑕疵检测中的行为机理，验证C3k2与C2PSA模块的有效性。
2. **方法层面**：提出一套针对PCB缺陷的改进YOLOv11算法（如命名为YOLOv11-PCB），通过P2头、BiFPN和WIoU的协同作用，显著提升微小缺陷的检出率。
3. **应用层面**：验证基于Stable Diffusion的生成式数据增强在工业质检中的可行性，并实现模型在边缘设备上的TensorRT加速部署，为工业现场应用提供参考原型。

### 6.2 建议的论文时间表

- **第1-2个月**：文献调研，复现YOLOv11 baseline，跑通DeepPCB数据集。
- **第3-4个月**：进行架构改进（P2头, Attention, BiFPN），完成消融实验。
- **第5个月**：研究Stable Diffusion数据增强，扩充数据集并重新训练。
- **第6个月**：边缘部署（Jetson），进行TensorRT加速与性能测试。
- **第7个月**：撰写论文，整理实验数据与图表。

通过遵循上述路线，您的毕业论文将不仅紧跟技术前沿（YOLOv11, GenAI），而且具有扎实的工程落地价值，完全符合高质量硕士/博士论文的标准。

------

**参考文献引用说明**： 本文综述了2024-2025年间的最新研究成果，涵盖了YOLOv11的官方发布文档 、相关的架构分析 、PCB检测领域的综述与改进算法 、以及边缘计算与生成式AI的应用 。所有建议均基于这些前沿文献的实证结果与理论推导。  

