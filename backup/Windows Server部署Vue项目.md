### 前期准备

购买服务器 （我选的是windows server)
给服务器配置公网ip(弹性ip)
学生有300优惠券(可白嫖）

### 远程连接服务器

1. win+r,输入mstsc，enter,

![image.png](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721270564830-69f19947-180f-4307-b155-4c247566a768.png#averageHue=%23f7f6f5&clientId=ud6cf2938-217d-4&from=paste&height=186&id=udea755ea&originHeight=279&originWidth=624&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=15574&status=done&style=none&taskId=u0fca104a-afb7-4c6f-ba12-aa3adf2a1ea&title=&width=416)

2. 输入服务器的公网IP，

![image.png](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721270592157-0a5ce2ff-f3ed-4b49-99da-c515876afd8b.png#averageHue=%23d8b790&clientId=ud6cf2938-217d-4&from=paste&height=310&id=uad0cb88b&originHeight=465&originWidth=771&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=62463&status=done&style=none&taskId=ua01328e2-ad42-48df-bec0-751f1a322a8&title=&width=514)

3. 用户名+密码 : administrator+password

![image.png](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721270618717-bb6b468e-0698-4594-88b6-57347b46ba2e.png#averageHue=%23a9c8b5&clientId=ud6cf2938-217d-4&from=paste&height=889&id=uf61bcd23&originHeight=1334&originWidth=2160&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=807605&status=done&style=none&taskId=u53323ce7-650d-4751-b834-9178fdb1164&title=&width=1440)
在主机和服务器之间可以通过 复制 粘贴传输文件

### 安装相关软件

![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1720785317151-4d8b8647-e22c-4caf-a785-7d36aa6fc256.png?x-oss-process=image%2Fformat%2Cwebp#averageHue=%23fbfaf9&from=url&id=wfOjC&originHeight=344&originWidth=1078&originalType=binary&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&title=)

#### bandzip(压缩软件）

#### nodejs

#### tomcat

（1）安装成功之后，Tomcat\apache-tomcat-10.0.16\bin里面，找到startup.bat文件，双击运行。
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062326233-b6371f85-eed2-4133-8ffa-15f86dfe1dc2.png#averageHue=%2333312f&clientId=uf7c6e7bb-3f7e-4&from=paste&id=uf4a9dcb5&originHeight=319&originWidth=1216&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=ufcfd9116-5880-4be4-a557-2d4a6608794&title=)
（2）在浏览器输入localhost:8080 出现如下页面说明Tomcat部署成功。
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062333871-6863008c-4bd5-42f0-a477-be7550f8a188.png#averageHue=%23d9f0c6&clientId=uf7c6e7bb-3f7e-4&from=paste&id=u41610923&originHeight=630&originWidth=1272&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=ufccd6670-9721-47ef-a1a7-59585d7c9fe&title=)
（3）最后一步，修改端口，8080是tomcat默认的端口，而80是常用的默认端口。如果端口设置为80的话，输入完ip后不需要接80。因为80已经设置为默认的端口了。
打开Tomcat所在的目录，打开conf文件夹，打开server.xml文件，如图，将port改为80：

```powershell
<Connector port="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
```

#### vscode

#### nginx

#### jdk

需要给jdk配置环境变量
安装完成之后，配置系统环境变量：如下图所示
（1）JAVA_HOME：服务器存放jdk文件的路径
（2）CLASSPATH: %JAVA_HOME%\lib\dt.jar;%JAVA_HOME%\lib\tools.jar
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721061924191-a23b45d1-4da0-45b2-8eef-15a06de60dfb.png#averageHue=%23f4f0ee&clientId=uf7c6e7bb-3f7e-4&from=paste&height=633&id=u16094707&originHeight=633&originWidth=696&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u78ff38a3-0565-453a-8f23-375d19e6a2f&title=&width=696)
（3）Path: %JAVA_HOME%\bin 和 %JAVA_HOME%\jre\bin
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721061962254-ae447341-7688-4e5e-aa0a-b130b7fae85c.png#averageHue=%23f2f0ef&clientId=uf7c6e7bb-3f7e-4&from=paste&id=u3e318ddb&originHeight=767&originWidth=861&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u8a815024-1804-46ed-bb79-f6e0ce8d4fa&title=)
最后，cmd 输入:java -version ，看是否出现版本消息，如图说明配置成功。
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721061973810-2ae9feeb-7ea0-40a1-88f4-2b9011a3f8c8.png#averageHue=%23393735&clientId=uf7c6e7bb-3f7e-4&from=paste&id=ucba9e790&originHeight=223&originWidth=656&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u8ce623bb-8fe8-4892-ab70-67827302a86&title=)
软件下载链接：
[[server.zip](https://www.yuque.com/attachments/yuque/0/2024/zip/40495483/1720785528282-53e587e2-707f-4437-973d-f4d7449363df.zip?_lake_card=%7B%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2024%2Fzip%2F40495483%2F1720785528282-53e587e2-707f-4437-973d-f4d7449363df.zip%22%2C%22name%22%3A%22server.zip%22%2C%22size%22%3A323477809%2C%22ext%22%3A%22zip%22%2C%22source%22%3A%22%22%2C%22status%22%3A%22done%22%2C%22download%22%3Atrue%2C%22taskId%22%3A%22u3904ccc2-c155-42db-91b3-19108667860%22%2C%22taskType%22%3A%22upload%22%2C%22type%22%3A%22application%2Fx-zip-compressed%22%2C%22__spacing%22%3A%22both%22%2C%22mode%22%3A%22title%22%2C%22id%22%3A%22uab99bd8b%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22file%22%7D)](https://www.yuque.com/attachments/yuque/0/2024/zip/40495483/1720785528282-53e587e2-707f-4437-973d-f4d7449363df.zip?_lake_card=%7B%22src%22%3A%22https%3A%2F%2Fwww.yuque.com%2Fattachments%2Fyuque%2F0%2F2024%2Fzip%2F40495483%2F1720785528282-53e587e2-707f-4437-973d-f4d7449363df.zip%22%2C%22name%22%3A%22server.zip%22%2C%22size%22%3A323477809%2C%22ext%22%3A%22zip%22%2C%22source%22%3A%22%22%2C%22status%22%3A%22done%22%2C%22download%22%3Atrue%2C%22taskId%22%3A%22u3904ccc2-c155-42db-91b3-19108667860%22%2C%22taskType%22%3A%22upload%22%2C%22type%22%3A%22application%2Fx-zip-compressed%22%2C%22__spacing%22%3A%22both%22%2C%22mode%22%3A%22title%22%2C%22id%22%3A%22uab99bd8b%22%2C%22margin%22%3A%7B%22top%22%3Atrue%2C%22bottom%22%3Atrue%7D%2C%22card%22%3A%22file%22%7D)

### 相关软件的配置

#### 配置IIS服务

1. 在云服务器ECS实例中打开CMD命令提示符。
2. 输入powershell切换至PowerShell模块。
3. 安装IIS服务及相关管理工具。

```powershell
Install-WindowsFeature -name Web-Server -IncludeAllSubFeature -IncludeManagementTools
```

4. IIS安装进度变为100%后，在当前浏览器页面，新开启一个网页，在地址栏输入实例的公网IP地址，并回车。

```shell
http://<实例公网IP地址>
```

参考连接：[https://help.aliyun.com/zh/ecs/getting-started/quick-start-for-windows-instances](https://help.aliyun.com/zh/ecs/getting-started/quick-start-for-windows-instances)

#### nginx配置

##### 1 配置

nginx默认的监听端口为80，如被占用可修改：” **nginx\conf\nginx.conf** “ 文件
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062534431-d417d0c7-4d79-401e-a6d8-5a3b11b3edcf.png#averageHue=%23f9f3f2&clientId=uf7c6e7bb-3f7e-4&from=paste&id=uce5e4df9&originHeight=286&originWidth=504&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=ub2e3777d-7f66-49b4-916d-7897ded6bf3&title=)

##### 2.启动

双击解压后根目录下的nginx.exe或命令行启动均可。
启动后，在浏览器输入 ” [[http://localhost:80](http://localhost/)](http://localhost/) " 进行测试
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062534393-769edbd3-56ee-41f0-9ec0-da85c71f39d9.png#averageHue=%23f5f4f3&clientId=uf7c6e7bb-3f7e-4&from=paste&id=u90451ac5&originHeight=296&originWidth=827&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u4d39b2ba-6b0d-4216-8ae1-7e2c66c0b5c&title=)

##### 3.关闭

由于未设置环境变量，关闭时需要利用命令行进入nginx所在路径，执行 “ **nginx -s stop** ”。
除了nginx外，还有其他的web服务器，不过nginx内存占用少，启动快，并发能力强，并且安装简单，因此采用nginx。
重启：“ **nginx -s reload** ”

### 项目打包

在vite.config.js中加入这个
![image.png](https://cdn.nlark.com/yuque/0/2024/png/40495483/1720788264803-7a2eb056-bdd0-43eb-a908-11eb6e0bc81c.png#averageHue=%231f2224&clientId=u7a6c5047-46a8-4&from=paste&height=745&id=u6dd19378&originHeight=1118&originWidth=983&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=145885&status=done&style=none&taskId=ue94e05a4-4e8b-49ed-8712-d1d19f2d0c7&title=&width=655.3333333333334)

图片的路径要特别注意
![image.png](https://cdn.nlark.com/yuque/0/2024/png/40495483/1720788495439-7b0deadc-85c6-4aaa-858c-4db1c2afc74d.png#averageHue=%231f2125&clientId=u7a6c5047-46a8-4&from=paste&height=665&id=ue62df5ec&originHeight=998&originWidth=978&originalType=binary&ratio=1.5&rotation=0&showTitle=false&size=202117&status=done&style=none&taskId=u797a945f-2c8e-4f5b-9e01-d597db46d7a&title=&width=652)
然后好像就没有问题了

```powershell
npm run build
```

### 部署到服务器

这里的端口记得要在阿里云平台的ECS的控制台给服务器配置安全组，即放行端口，不然是无法访问到我们的网页的

#### 使用tomcat

把生成的dist文件移动到tomcat的webapps下，运行startup.bat
即可http://<公网ip>:port/<项目名>  访问

#### 使用nginx

将build生成的dist目录复制到nginx下的html目录中。
修改nginx配置文件
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062558742-dc5a06ac-94ce-45bd-94bc-92868d1d09f6.png#averageHue=%23202020&clientId=uf7c6e7bb-3f7e-4&from=paste&id=kdjUb&originHeight=324&originWidth=719&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u545d3232-017a-487c-8625-c692be2d5c6&title=)
重启nginx，浏览器访问 “ [http://localhost:8080/](http://localhost:8080/) ”，即可。
如果页面空白，没有任何内容，使用F12查看报错信息
![](https://cdn.nlark.com/yuque/0/2024/png/40495483/1721062558752-72dae101-ccaf-410c-83f1-35e8a9005000.png#averageHue=%23f9f6e4&clientId=uf7c6e7bb-3f7e-4&from=paste&id=Xnvqp&originHeight=125&originWidth=787&originalType=url&ratio=1.5&rotation=0&showTitle=false&status=done&style=none&taskId=u5fdf6904-3e78-4e3e-82c9-37d52e8905d&title=)
如果错误如上图所示，恭喜你，很好解决，这是因为打包找寻路径错误，导致dist中的index.html中的css与js加载失败。
回到vue项目中，打开 **vue.config.js** 文件

```
module.exports = {
  publicPath: '/myName'
};
```

如果你的配置做了修改，没有使用默认配置（如上），则表明资源加载路径为 ' **/myName** '，此时有两个方法：

1. 将**publicPath**恢复成默认状态：`publicPath: './'`（不建议）；
2. 重新配置nginx。

这里建议使用第二种方法，因为nginx可能会部署多个项目，针对不同项目增加配置是一种很正常的操作。
打开**nginx.conf**文件

```shell
server {
        listen       8080; # 监听的端口号，默认是8080
        server_name  localhost; # 默认地址，仅需要在本地做验证，可以不修改

		# 这里可以放nginx启动页
        location / {
            root   html/dist; # 项目所在路径
            index  index.html index.htm; # 默认访问主页
            try_files  $uri $uri/ index.html=404; # 解决vue项目刷新404的问题
        }

		# 这里放新增加的项目，我这里叫myName，因此localtion后接/myName
        location /myName {
            alias  html/myName; # 项目所在路径
            index  index.html index.htm; # 默认访问主页
            try_files  $uri $uri/ /myName/index.html; # 解决vue项目刷新404的问题
        }
}
```

之后，将打包后的dist文件更名为myName，重启nginx，访问链接[http://localhost:8080/myName/](http://localhost:8080/myName/)
参考文章：
[https://blog.csdn.net/weixin_43690623/article/details/122718677](https://blog.csdn.net/weixin_43690623/article/details/122718677)
[https://www.cnblogs.com/quantoublog/articles/17998376](https://www.cnblogs.com/quantoublog/articles/17998376)