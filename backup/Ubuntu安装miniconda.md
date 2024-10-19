## 一、下载安装miniconda

```cpp
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh
```

## 二、安装 Miniconda 后设置环境变量

### 1. 检查安装路径
首先，确认 Miniconda 的安装路径。默认情况下，Miniconda 会安装在你的用户主目录下，路径通常是 `~/miniconda3`。
```bash
ls ~/miniconda3
```
如果路径不同，请替换下面的命令中的 `~/miniconda3` 为你实际的安装路径。
### 2. 添加 Miniconda 到环境变量
编辑你的 `.bashrc` 文件，添加 Miniconda 的路径到 `PATH` 环境变量中。
```bash
echo 'export PATH="/home/tanbin/miniconda3/bin:$PATH"' >> ~/.bashrc
```
### 3. 重新加载 `.bashrc` 文件
重新加载 `.bashrc` 文件以使更改生效。
```bash
source ~/.bashrc
```
### 4. 验证 `conda` 命令
再次尝试运行 `conda` 命令，看看是否已经可以正常使用。
```bash
conda --version
```
### 5. 初始化 Conda（可选）
如果你选择不在安装过程中初始化 Conda，可以手动初始化它。这将确保 Conda 的 shell 函数被正确加载。
```bash
conda init
```
### 6. 重新启动终端
有时，重新启动终端可以确保所有更改生效。