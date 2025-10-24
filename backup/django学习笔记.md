# Diango学习笔记

采用Anaconda+Pycharm实现

安装Diango：
[[Diango学习笔记]]

```powershell
pip install django

or

conda install diango
```

## 一、建立项目

### (一)打开powershell

```powershell
win+r
```

### (二)进入到我们想要存放文件的目录

```powershell
cd PycharmProjects
```

可以看到如下输出：

```powershell
C:\Users\tb>cd PycharmProjects
C:\Users\tb\PycharmProjects>
```

### (三)在Django中创建项目

```powershell
django-admin startproject learning_log .

dir

dir learning_log
```

(注意不要忘记上面的句点)

这行代码将会在当前目录下创建一个 `learning_logs` 目录。如果命令失败了，查看 [运行 django-admin 时遇到的问题](https://docs.djangoproject.com/zh-hans/4.2/faq/troubleshooting/#troubleshooting-django-admin)，可能能给你提供帮助。

### (四)创建数据库

```powershell
python manage.py migrate

ls
```

### (五)查看项目

```powershell
python manage.py runserver
```

你应该会看到如下输出：

```powershell
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

七月 24, 2023 - 15:50:53
Django version 4.2, using settings 'mysite.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

点击下面链接可查看    http://127.0.0.1:8000/ 

注意：在后续的步骤中该CMD窗口最好不要关闭，后续的操作中要打开新的CMD窗口输入命令

## 二、创建应用程序

再打开一个终端窗口，切换到manage.py所在的目录

```powershell
cd PyCharmProjects

python manage.py startapp learning_logs

dir
```

会看到如下输出：

```powershell
PS C:\Users\tb\PycharmProjects> dir

    目录: C:\Users\tb\PycharmProjects

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2023/7/25     15:37                learning_log
d-----         2023/7/25     15:39                learning_logs
d-----         2023/7/24     15:55                pythonProject
d-----         2023/7/25     12:09                pythonProject1
-a----         2023/7/25     15:37         131072 db.sqlite3
-a----         2023/7/25     15:35            690 manage.py
```

再输入

```powershell
dir learning_logs/
```

会看到如下输出：

```powershell
PS C:\Users\tb\PycharmProjects> dir learning_logs/

    目录: C:\Users\tb\PycharmProjects\learning_logs

Mode                 LastWriteTime         Length Name
----                 -------------         ------ ----
d-----         2023/7/25     15:39                migrations
-a----         2023/7/25     15:39             66 admin.py
-a----         2023/7/25     15:39            163 apps.py
-a----         2023/7/25     15:39             60 models.py
-a----         2023/7/25     15:39             63 tests.py
-a----         2023/7/25     15:39             66 views.py
-a----         2023/7/25     15:39              0 __init__.py
```

### (一)定义模型

打开文件models.py,创建自己的模型

创建了Topic、Entry两个类，它们都继承Model

```python
from django.db import models

# Create your models here.
class Topic(models.Model):
    '''用户学习的主题'''
    text = models.CharField(max_length=200) #由字符组成的数据
    date_added = models.DateTimeField(auto_now_add=True) #记录时间和日期的数据

    def __str__(self):
        return self.text

class Entry(models.Model):
    '''学到的有关某个主题的具体知识'''
    topic = models.ForeignKey(Topic, on_delete=models.CASCADE)
    text = models.TextField()
    date_added = models.DateTimeField(auto_now_add=True)
    class Meta:
        verbose_name_plural = 'entries'

    def __str__(self):
        return f"{self.text[:50]}..."
```

### (二)激活模型

打开setting.py,将

```python
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

修改为：

```python
INSTALLED_APPS = [
    #我的应用程序
    "learning_logs",

    #默认应用程序
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]
```

(三)让Django修改数据库，使其能够存储与模型Topic、Entry相关的信息，在CMD窗口中执行如下命令：

```powershell
python manage.py makemigrations learning_logs

python manage.py migrate
```

```powershell
PS C:\Users\tb\PycharmProjects> python manage.py makemigrations learning_logs
Migrations for 'learning_logs':
  learning_logs\migrations\0001_initial.py
    - Create model Topic


PS C:\Users\tb\PycharmProjects> python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, learning_logs, sessions
Running migrations:
  Applying learning_logs.0001_initial... OK
```

注意：在后面每次增加新模型后，都需要迁移数据库：修改models.py，执行命令

```powershell
python manage.py makemigrations learning_logs

python manage.py migrate
```

### (三)Django管理网站

#### 1、创建超级用户（具备所有权限的用户）

在cmd中输入命令：

```powershell
python manage.py createsuperuser
```

可以看到如下输出：输入Username，Email，Password

```powershell
PS C:\Users\tb\PycharmProjects> python manage.py createsuperuser
Username (leave blank to use 'tb'): tb
Email address: your email
Password:
Password (again):
Superuser created successfully.
PS C:\Users\tb\PycharmProjects>  python manage.py makemigrations learning_logs
Migrations for 'learning_logs':
  learning_logs\migrations\0002_entry.py
    - Create model Entry
```

#### 2、向网站注册模型

Django会自动向网站中添加模型，如User和Group,但是我们自己创建的模型，需要手动注册。打开admin.py

```python
from django.contrib import admin

# Register your models here.
```

添加如下语句：

```python
from django.contrib import admin
from .models import Topic,Entry

# Register your models here.
admin.site.register(Topic)
admin.site.register(Entry)
```

#### 3、使用超级用户账户访问网站

访问如下链接

http://localhost:8000/admin/ （推荐）或者https://localhost:8000/admin/ (不推荐，有可能会打不开)

输入username和password登录

#### 4、添加主题

![](D:\Huawei Share\Screenshot\capture_20230725172223431.bmp)

Diango（Django的中文拼写）是一个流行的Python Web框架，用于快速开发高质量的Web应用程序。它遵循“MTV”（Model-Template-View）的设计模式，提供了丰富的功能和工具，使Web开发变得更加简单和高效。

下面是一些Django的入门操作步骤：

1. 确保安装Python：首先，确保你的计算机上已经安装了Python。Django需要Python 3.6或更高版本。
2. 安装Django：使用以下命令在命令行或终端中安装Django（假设你已经安装了Python）：

```
Copy code
pip install django
```

1. 创建Django项目：在命令行中，导航到你想要创建项目的目录，并运行以下命令来创建Django项目：

```
Copy code
django-admin startproject projectname
```

这将在当前目录下创建一个名为"projectname"的Django项目。

1. 运行开发服务器：进入项目目录，执行以下命令来启动Django开发服务器：

```
bashCopy codecd projectname
python manage.py runserver
```

现在，你可以通过浏览器访问`http://127.0.0.1:8000/`来查看Django默认的欢迎页面。

1. 创建Django应用：Django项目可以包含多个应用程序。要创建一个应用程序，请运行以下命令：

```
Copy code
python manage.py startapp appname
```

这将在项目目录下创建一个名为"appname"的Django应用程序。

1. 定义模型：在Django中，模型用于定义数据结构。打开"appname/models.py"文件，并定义你的模型类。
2. 迁移数据库：在定义了模型之后，运行以下命令以创建数据库表格：

```
Copy codepython manage.py makemigrations
python manage.py migrate
```

这将根据你在模型中定义的内容，生成数据库表格。

1. 创建视图：在Django中，视图处理Web请求并返回响应。打开"appname/views.py"文件，并编写你的视图函数。
2. 创建URL映射：为了让Django知道如何将URL映射到视图，打开"appname/urls.py"文件，并设置URL路由。
3. 运行你的应用：启动开发服务器后，你就可以通过定义的URL来访问你的应用程序。

这只是Django的入门操作，Django还有很多功能和特性可以探索，如静态文件处理、表单、认证、管理后台等。你可以参考官方文档（https://docs.djangoproject.com/）和其他教程深入了解Django的更多内容。祝你在Django的世界里编写出优秀的Web应用程序！
