### .NET Core开发、运行环境的安装
对于初学者来说，选择一个语言，然后这个语言所对应的运行平台，使用这个语言编写程序代码的编辑器都是我们考虑的重点。如果你看到我这篇文章，你很幸运，无论你是其它任何语言，在集成开发工具方面，C#使用的开发工具，开发出来的应用程序的运行环境，在安装和使用上都是非常方便的。
而我们所说的.NET是一个运行平台，在这个平台之上可以使用c#作为开发语言来编写你的应用程序。  
现在.NET已经支持多操作系统了，只要在对应的操作系统上安装对应的运行时环境，就可以运行起你的应用程序了，做到了一处编译，到处运行的好处。  

C#开发环境的首选操作系统是Windows，其次就mac OS,建议不要使用linux，而在运行环境的选择来说：建议首选择linux，其次是windows，暂时还没有看到很大规模的应用程序运行在以mac OS的操作系统之上。  

下面分别介绍Windows的开发环境与linux运行开发工具包和运行时平台的安装;  
如需要转发请标明出处，本系列文章首发于[github.com/chenzuo](https://github.com/chenzuo/dotnet-core-practices);联系方式：chenzuo@hotmail.com;
#### 在windows下安装SDK开发包和集成开发工具
熟悉使用winodws的同学都非常了解windows软件的安装使用，所以这儿我就直接贴出安装包下载地址：  
+ 集成开发工具下载：[Visual Studio 2019](https://visualstudio.microsoft.com/zh-hans/downloads/).建议下载企业版本，不要问为什么，照做即可:)
+ SDK工具包下载地址：[.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/thank-you/dotnet-sdk-2.2.300-windows-x64-installer,.NET),如果你开发环境是Visual Studio 2017，那么你需要下载是安装包是：[.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/thank-you/dotnet-sdk-2.2.107-windows-x64-installer)  
+ .NET版本对应的安装包地址：[dotnet-core](https://dotnet.microsoft.com/download/dotnet-core/2.2#sdk-2.2.107)  
+ 开发工具对应的 .NET Core安装包环境下载地址：[Visual Studio SDK For .NET Core ](https://dotnet.microsoft.com/download/visual-studio-sdks)

以上是下载地址，你可以选择对应SDK或开发工具然后根据你在windows使用经验进行安装吧:)
#### 在linux操作系统上安装.NET Core运行时环境
在.NET Core未出世前，我们都是在windows开发与运行，但是 .NET Core出来后，改变了我们之前的一惯作法，我们可以把开发好的应用程序部署在linux下运行（前提是必须是在.NET Core下编译通过的），那么在linux下安装 .NET Core运行时，也是非常简单，只需要你使用对应安装命令即可，我们推荐使用centos7.0以上的版本，当然你可以使用ubuntu系统，centos操作系统正安装运行时命令是： 
运行安装前，建议清理系统中的源加载：
```sh
# rm -fr /var/cache/yum/*
# yum clean all
``` 
或者参考链接：
Why does yum return error: [Errno 256] No more mirrors to try.[Url](https://rmohan.com/?p=4755)  
在系统中注册:microsoft product repository:
```sh
sudo rpm -Uvh https://packages.microsoft.com/config/rhel/7/packages-microsoft-prod.rpm
```
安装运行时:
```sh
sudo yum update  
sudo yum install aspnetcore-runtime-2.2
```
这样就已经准备好了使用C#语言在.NET Core平台上的开发环境与运行环境。

####  linux常规操作命令集整理
+ 列出当前目录下所有文件与目录  
```sh
ls
```
+ 防火墙操作
```sh
启动： systemctl start firewalld
关闭： systemctl stop firewalld
查看状态： systemctl status firewalld
开机禁用  ： systemctl disable firewalld
开机启用  ： systemctl enable firewalld

启动一个服务：systemctl start firewalld.service
关闭一个服务：systemctl stop firewalld.service
重启一个服务：systemctl restart firewalld.service
显示一个服务的状态：systemctl status firewalld.service
在开机时启用一个服务：systemctl enable firewalld.service
在开机时禁用一个服务：systemctl disable firewalld.service
查看服务是否开机启动：systemctl is-enabled firewalld.service
查看已启动的服务列表：systemctl list-unit-files|grep enabled
查看启动失败的服务列表：systemctl --failed

查看版本： firewall-cmd --version
查看帮助： firewall-cmd --help
显示状态： firewall-cmd --state
查看所有打开的端口： firewall-cmd --zone=public --list-ports
更新防火墙规则： firewall-cmd --reload
查看区域信息:  firewall-cmd --get-active-zones
查看指定接口所属区域： firewall-cmd --get-zone-of-interface=eth0
拒绝所有包：firewall-cmd --panic-on
取消拒绝状态： firewall-cmd --panic-off
查看是否拒绝： firewall-cmd --query-panic

添加：firewall-cmd --zone=public --add-port=80/tcp --permanent （--permanent永久生效，没有此参数重启后失效）
重新载入
firewall-cmd --reload
查看：firewall-cmd --zone=public --query-port=80/tcp
删除：firewall-cmd --zone=public --remove-port=80/tcp --permanent

```