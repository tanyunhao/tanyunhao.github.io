背景：

日常使用Typora写markdown笔记，会经常插入图片，来帮助理解和整理逻辑。

但是图片保存在本地，上传到网上时，就面临图片不见，或者错误警告等等。

所以将图片上传到网上，做成一个图床来保证图片的有效性是非常重要的。

### 安装：

1. 打开Typora的偏好设置，mac在屏幕最上面的Typora选项，偏好设置，点击图像。

![](https://pic3.zhimg.com/80/v2-5624dccafa5f9739dc01d7739c051e3a_1440w.webp)

2. 在上传服务中点击Custom Command  

3. 打开终端，输入以下命令。  

```powershell
#安装picgo-core（如果没装npm，先安装，centos下是yum install npm）    
npm install picgo -g    

#查看node和picgo的路径    
which node    
which picgo    

#将得到的路径按照以下格式写入第三步的自定义命令中。(中间要有空格)    
/usr/local/bin/node /usr/local/bin/picgo upload 
```

4. 注册一个码云（gitee）账号  

5. 创建一个仓库（加号）  

![](https://pic4.zhimg.com/80/v2-c195932371bf9cb93619ba41e8db18d3_1440w.webp)

6. 仓库设定

![](https://pic3.zhimg.com/80/v2-e6b796bb8922aae61cb1eb17b57e84d2_1440w.webp)

7. 新建token，点击头像

![](https://pic4.zhimg.com/80/v2-c195932371bf9cb93619ba41e8db18d3_1440w.webp)

![](https://pic1.zhimg.com/80/v2-08ec2892542c0e823bb623c8a400b920_1440w.webp)

![](https://pic1.zhimg.com/80/v2-6502f9cd5aa82fb3fda6bb958c418298_1440w.webp)

8. 开始设定picgo配置文件

打开终端输入以下命令

```powershell
#安装gitee的插件    
picgo install gitee-uploader 

#设置配置文件    
picgo set uploader  

1.按上下键找到gitee，回车    
2.repo：用户名/仓库名 （打开自己的仓库，浏览器里的网址username/reponame）    
3.token：刚才生成的token    
4.path:路径，写仓库的名字就是reponame    
5.custompath:不用填，回车   
6.customURL:不用填，回车    

#使用配置好的文件（配置文件在~/.picgo/config.json）    
picgo use uploader
```

9. 打开你typora，验证图片上传，查看是否成功。

![](https://pic3.zhimg.com/80/v2-4aed1fba7ef586b51ec01fa0008aff2e_1440w.webp)

10. 成功设置好图床，将一张图片拖到typora中，试一下能否自动上传，注意不要批量上传，会导致错误。