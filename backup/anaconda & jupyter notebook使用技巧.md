
# anaconda & jupyter notebook使用技巧

## 一、安装

### anaconda安装：

https://www.anaconda.com/

安装教程：https://blog.csdn.net/qq_42257666/article/details/121383450

### jupyter notebook:

anaconda会自行绑定jupyter notebook和spyder,开箱即用

Readme

## 二、配置环境

[Anaconda3安装教程与环境变量添加 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/597981788)

## 三、jupyter notebook安装插件

首先我们先下载好插件选择的工具栏，通过`pip install`来进行下载即可

```powershell
pip install jupyter_contrib_nbextension
```

```
pip install -i https://pypi.tuna.tsinghua.edu.cn/simple jupyter_contrib_nbextensions
```

然后我们将这个插件选项的工具栏添加到`jupyter notebook`的页面当中，运行下面这个的命令行

必须要有这一步，否则在jupyter notebook中看不到Nbextensions

```powershell
jupyter contrib nbextension install
```

s我们打开`jupyter notebook`页面之后就可以看到有`Nbextensions`这个工具栏

然后就可以安装插件了

## 四、jupyter notebook更换主题

打开anaconda propmt,输入

```powershell
pip install --upgrade jupyterthemes
```

输入命令查看主题列表

```powershell
jt -l
```

会看到如下输出

```powershell
Available Themes:
   chesterish
   grade3
   gruvboxd
   gruvboxl
   monokai
   oceans16
   onedork
   solarizedd
   solarizedl
```

输入命令切换主题：

```powershell
jt -t [theme] -T

jt -t monokai -T

jt -t gruvboxl -T

jt -t chesterish -T


```

```
jt -t monokai -T -f roboto -fs 14 -nfs 14 -tfs 14 -ofs 11
```
## 五、jupyter notebook使用Anaconda虚拟环境内核

创建一个名为 "yourenvname" 的 Conda 环境，并在该环境中安装 pycaret 软件包，并且将该环境注册为 Jupyter Notebook 的内核的一系列命令。

### 1.创建一个名为 "yourenvname" 的 Conda 环境，并指定 Python 版本为 3.8：

```powershell
conda create --name yourenvname python=3.8
```

这个命令会在 Conda 环境中创建一个名为 "yourenvname" 的全新环境，其中包含了 Python 3.8 版本。

### 2.激活 "yourenvname" 环境：

```powershell
conda activate yourenvname
```

这个命令用于激活刚刚创建的 "yourenvname" 环境，意味着在后续的操作中，将在yourenvname环境下进行工作。

### 3.在 "yourenvname" 环境中安装 pycaret：

```powershell
pip install pycaret
```

这个命令使用 pip 包管理器在激活的 "yourenvname" 环境中安装了 pycaret 软件包。Pycaret 是一个用于快速和简单地进行机器学习任务的库。

### 4.创建 Jupyter Notebook 的内核：



```powershell
python -m ipykernel install --user --name mytorch --display-name "mytorch"
```

```bash
python -m ipykernel install --user --name mytorch --display-name "myenv"
```

这个命令用于在 Jupyter Notebook 中创建一个新的内核，使得您可以在该环境下运行 Notebook。"yourenvname" 参数指定了 Conda 环境的名称，"display-name" 参数用于指定内核在 Notebook 中显示的名称。

综上所述，这些命令将会在 Conda 环境中安装 pycaret 并在 Jupyter Notebook 中创建一个新的内核，以便可以在该环境中进行机器学习任务和分析。

### 5.查看 Jupyter notebook kernel

```py
jupyter kernelspec list
1
```

![在这里插入图片描述](https://gitee.com/huake-tan-yunhao/picture/raw/master/picture/20200830215814833.png)

### 6.删除 jupyter 内核

```py
jupyter kernelspec remove kernelname
```

## Pytorch和TensorFlow

[[pytorch和TensorFlow安装教程]]

# YOLOv8
```
conda create --name YOLO python=3.11
```

```
conda activate YOLO
```

conda create --name collective-intelligence python=3.11