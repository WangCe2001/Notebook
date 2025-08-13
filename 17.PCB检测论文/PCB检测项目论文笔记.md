# 一.Anaconda环境操作

列出环境：

```bash
conda env list
```

删除环境：

```bash
conda env remove --name <your_env_name>
```

创建环境：使用**Python=3.11**环境

```bash
conda create -n yolo_env python=3.11 -y
```

激活环境：

```bash
conda activate yolo_v11
```

打开cmd命令行，查看CUDA driver版本：需要**CUDA runtime version <= CUDA driver version**

```bash
nvidia-smi
```

![image-20250804110355609](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250804110355609.png)

进入维基百科，根据算例选择对应的CUDA runtime version：https://en.wikipedia.org/wiki/CUDA

本电脑对应算例为8.9，故选择CUDA=12.6版本

Pytorch官网：https://pytorch.org/get-started/locally/

```bash
pip3 install torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu126
```

检验是否安装成功：

```bash
python
import torch
torch.cuda.is_available()
exit()
```

![image-20250804111741634](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250804111741634.png)

安装ultralytics，参考链接：https://docs.ultralytics.com/quickstart/

```bash
# Install the ultralytics package from PyPI
pip install ultralytics
```

下载yolov11压缩包，参考链接：https://github.com/ultralytics/ultralytics

文件路径：D:\09.YOLO\02.ultralytics\ultralytics-main

使用pycharm打开项目





# 二.上传至Github

1.在本机电脑中配置SSH，并添加到GitHub中，配置过程参考视频教学

2.使用pycharm中的版本控制来进行

## 第一步：在 PyCharm 中将你的项目初始化为 Git 仓库

这是告诉 Git：“嘿，请开始管理我这个项目文件夹吧！”

1. 用 PyCharm 打开你现有的 Python 项目。
2. 点击顶部菜单栏的 `VCS` (Version Control System)。
3. 在下拉菜单中，选择 `Enable Version Control Integration...`。
4. 在弹出的窗口中，从下拉菜单里选择 `Git`，然后点击 `OK`。
5. **观察变化**：你会发现，项目视图里的所有文件名都变成了**红色**。这表示这些文件已经被 Git "看到"了，但它们还没有被正式地“暂存”或“提交”。

## 第二步：创建 `.gitignore` 文件并进行首次提交

在提交代码前，我们必须告诉 Git 哪些文件是**不需要**管理的，比如虚拟环境文件夹 (`venv`)、PyCharm 的配置 (`.idea`)、Python 的缓存 (`__pycache__`) 等。

1. **创建 `.gitignore` 文件**：

   - 在 PyCharm 的项目视图中，右键点击项目的根目录，选择 `New` -> `File`。
   - 文件名输入 `.gitignore` (注意，前面有个点)。
   - 将下面这段推荐的 Python 项目配置粘贴到 `.gitignore` 文件中并保存。

   代码段

   ```
   # PyCharm
   .idea/
   
   # Python
   __pycache__/
   *.pyc
   .env
   venv/
   env/
   
   # Build artifacts
   build/
   dist/
   *.egg-info/
   ```

2. **暂存并提交 (Commit)**：这是 Git 的核心操作，相当于创建一个“存档点”。

   - 打开 `Commit` 窗口。你可以通过左侧边栏的 `Commit` 标签打开它，或者使用快捷键 `Ctrl + K` (Windows/Linux) / `Cmd + K` (macOS)。
   - 在 `Changes` 列表中，你会看到项目里的所有文件（`.gitignore` 文件本身也会在里面）。勾选你想要提交的所有文件。通常，第一次提交会勾选全部文件。
   - **重要**：在 `Commit Message` 输入框里，写下本次提交的描述信息。对于第一次提交，通常写 `Initial commit`。**写好提交信息是一个非常重要的习惯！**
   - 点击 `Commit` 按钮。

   提交后，你会发现文件名都变回了正常的颜色（通常是白色或黑色），这表示你的代码已经有了一个本地的、安全的版本记录。

## 第三步：在 GitHub 上创建远程仓库

现在，我们需要在 GitHub 网站上为你的项目创建一个“家”。

1. 登录 GitHub，点击右上角的 `+` 号，选择 `New repository`。
2. **填写仓库信息**：
   - `Repository name`：最好和你的本地项目文件夹同名，这样不容易混淆。
   - `Description`：简单描述一下你的项目是做什么的。
   - 选择 `Public` (公开) 或 `Private` (私有)。
   - **非常重要**：**不要**勾选 "Add a README file", "Add .gitignore", "Choose a license"。因为你的本地项目已经有这些了，我们需要一个完全**空**的仓库来接收你的上传。
3. 点击 `Create repository`。
4. 创建成功后，页面会跳转到一个显示仓库地址的页面。找到并复制那个 HTTPS 地址，它看起来像这样：`https://github.com/YourUsername/YourProjectName.git`。

## 第四步：连接本地仓库到远程仓库并推送

这是最后一步，将你本地的“存档”上传到 GitHub。

1. 回到 PyCharm。
2. 点击顶部菜单栏的 `Git` -> `Manage Remotes...`。
3. 在弹出的 `Git Remotes` 窗口中，点击 `+` 号。
4. 在 `Add Remote` 窗口中：
   - `Name`：输入 `origin` (这是一个标准的、通用的命名习惯，代表你的主要远程仓库)。
   - `URL`：粘贴你刚刚从 GitHub 复制的仓库地址。
   - 点击 `OK` 保存。
5. **推送 (Push)**：
   - 现在，我们要把本地的提交推送到远程的 `origin`。
   - 点击顶部菜单栏的 `Git` -> `Push...`，或者使用快捷键 `Ctrl + Shift + K` (Windows/Linux) / `Cmd + Shift + K` (macOS)。
   - 在 `Push Commits` 窗口中，PyCharm 会显示你要推送的分支（比如 `main -> origin/main`）。确认无误后，点击 `Push`。
   - 如果这是你第一次向这个仓库推送，PyCharm 可能会需要你验证 GitHub 身份，按照提示操作即可。
6. **验证成功**：推送完成后，回到你在 GitHub 上的项目页面，刷新一下。你会惊喜地发现，你本地项目的所有文件都已经出现在 GitHub 上了！



# 三.下载PCB瑕疵数据集

下载网址：https://aistudio.baidu.com/datasetdetail/272346

有JSON格式和VOC两种格式

# 四.安装Label-Studio

使用anaconda安装过程：https://github.com/HumanSignal/label-studio

```bash
conda create --name label-studio
conda activate label-studio
conda install psycopg2
pip install label-studio
```

安装成功后打开步骤：

## 总结与日常使用建议

- **日常启动流程**：

  1. 打开 Anaconda Prompt 或终端。
  2. `conda activate label-studio` (激活环境)
  3. `cd /path/to/your/projects` (**建议**：先进入你打算存放标注项目的文件夹) 

     ```
     D：
     cd D:\09.YOLO\03.pcb_dataset\PCB_DATASET
     ```
  4. `label-studio start` (启动服务)

- **数据存放位置**：在你运行 `label-studio start` 命令的**当前目录下**，Label Studio 会自动创建一个名为 `label_studio.sqlite3` 的数据库文件和一些项目文件夹，用来存储你的所有项目和标注数据。所以，**强烈建议**先用 `cd` 命令进入一个专门的工作目录再启动它，以方便管理。

- **如何更新**：如果未来 Label Studio 发布了新版本，你只需要激活环境后，运行以下命令即可升级：

  Bash

  ```
  pip install --upgrade label-studio
  ```

- **机器学习后端**：如果你想使用 Label Studio 强大的机器学习辅助标注功能，你需要在**同一个 `label-studio-env` 环境中**安装相应的库（如 `tensorflow`, `pytorch`）和 `label-studio-ml-backend`。

这个流程可以确保你的 Label Studio 有一个干净、稳定且易于管理的环境。祝你使用愉快！



# 五.使用Label-Studio打开图片

## 1.配置本地仓库

如果配置过程中出现了报错，可以问Gemini来解决，解决步骤如下：

### 方法一：永久性解决方案（推荐）

这个方法的原理是：利用Anaconda环境的特性，创建一个脚本。每当您激活这个特定的Conda环境时，脚本会自动设置所需的环境变量。一劳永逸。

**步骤 1：打开Anaconda Prompt并激活环境**

1. 从Windows开始菜单找到并打开 **Anaconda Prompt** (不要使用普通的CMD或PowerShell)。

2. 激活您安装了Label Studio的Conda环境。假设您的环境名叫 `label-studio-env`（请替换成您自己的环境名）。

   Bash

   ```
   conda activate label-studio
   ```

**步骤 2：创建环境变量设置脚本**

1. 激活环境后，我们需要在环境的特定文件夹下创建一个批处理文件（`.bat`）。请依次执行以下命令来创建文件夹和文件：

   - 首先，创建 `activate.d` 文件夹（如果它不存在）：

     Bash

     ```
     mkdir "%CONDA_PREFIX%\etc\conda\activate.d"
     ```

     *(这里的 `%CONDA_PREFIX%` 是一个会自动指向当前激活环境路径的变量，您无需修改它)*

   - 然后，用记事本创建一个新的批处理文件：

     Bash

     ```
     notepad "%CONDA_PREFIX%\etc\conda\activate.d\env_vars.bat"
     ```

2. 在弹出的记事本窗口中，**复制并粘贴**以下内容：

   代码段

   ```
   @echo off
   set "LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED=true"
   set "LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT=D:\09.YOLO"
   ```

   **请注意**：

   - 第二行代码就是解决您问题的关键。
   - 第三行是**强烈推荐**的安全设置。请将 `D:\09.YOLO` 修改为您存放所有标注项目数据的**根目录**。这可以防止Label Studio访问到这个文件夹之外的其他文件。如果您的PCB数据就放在 `D:\09.YOLO` 下，那么这个设置就是完美的。

3. 保存记事本文件并关闭。

**步骤 3：创建环境变量清理脚本（好习惯）**

为了保持环境干净，我们再创建一个脚本，在您退出Conda环境时自动清除这些变量。

1. 同样在Anaconda Prompt中，执行以下命令：

   Bash

   ```
   mkdir "%CONDA_PREFIX%\etc\conda\deactivate.d"
   notepad "%CONDA_PREFIX%\etc\conda\deactivate.d\env_vars.bat"
   ```

2. 在弹出的记事本中，粘贴以下内容来“取消”设置：

   代码段

   ```
   @echo off
   set "LABEL_STUDIO_LOCAL_FILES_SERVING_ENABLED="
   set "LABEL_STUDIO_LOCAL_FILES_DOCUMENT_ROOT="
   ```

3. 保存并关闭记事本。

**步骤 4：验证并启动**

1. 现在，设置已经完成！为了让它生效，请先退出当前环境，再重新激活。

   Bash

   ```
   conda deactivate
   conda activate label-studio
   ```

2. 当您重新激活时，脚本会自动运行。现在您可以直接启动Label Studio了：

   Bash

   ```
   label-studio start
   ```

现在，回到Label Studio的网页界面，再次添加本地存储 `D:\09.YOLO\03.pcb_data`，它将不再报错，可以成功添加。以后您每次激活这个环境并启动Label Studio，这个设置都会自动生效。

![image-20250812110035172](https://typora-picture-wang.oss-cn-shanghai.aliyuncs.com/image-20250812110035172.png)
