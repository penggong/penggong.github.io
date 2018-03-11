---
layout:     post
title:      "Linux环境准备"
subtitle:   ""
date:       2018-03-07 14:00
author:     "parkin"
header-img: "img/post-bg-js-module"
catalog: ture
tags:
    - linux
---
# Linux环境准备

------

> *目录
一、 说明 3
二、 系统配置 3
三、 安装步骤 3
1 JDK的安装 3
1.1 创建java目录 3
1.2 上传JDK安装包至 /usr/java目录下 4
1.3 解压JDK安装包 6
1.4 配置环境变量 6
2 Tomcat的安装和配置 7
2.1 Tomact安装包上传 7
2.2 解压tomcat安装包及项目包上传 7
2.3 修改配置信息 8
2.3.1 Tomcat默认端口号修改（默认为8080） 8
2.3.2 修改链接字符串 8
2.3.3 修改报表链接字符串 9
2.3.4 配置完成后运行startup.sh即可 9
2.3.5 系统配置修改 9
3 OpenOffice安装 10
3.1 上传安装包并解压 10
3.2 安装 10
3.3 启动 11


# 一、说明

本文章旨在引导项目环境准备工作的顺利执行。

# 二、 系统配置

系统环境 Red Hat Enterprise 6.5
容器 tomcat7
数据库 oracle 11G R2

# 三、安装步骤

目录对应表：
tomcat /opt
jdk /usr/java
app /opt/apache-tomcat-7.0.69/webapps
注释：该操作中Linux命令在终端中操作，可使用SecureCRT等软件。

##1 JDK的安装
###1.1 创建java目录
命令：mkdir /usr/java

###1.2 上传JDK安装包至 /usr/java目录下
使用Xmanager软件

选择xftp

点击左上角新建，弹出新建窗口

出现如下界面，分别输入名称(自定义)，主机出填写Linux主机IP地址，协议选择SFTP，在下方用户名和密码处填写相应信息

信息填写完毕后，选择刚才新建的链接，点击连接

连接成功后进入如下界面，并选择进入到刚才建立的目录下/usr/java

在左侧选择Linux版本JDK的安装包后拖放至右侧目录下，等待上传完毕。
###1.3 解压JDK安装包
进入到上传的目录下，解压JDK
使用命令：
```
tar -xvf jdk-7u79-linux-x64.tar
```
解压完毕后目录下会出现文件夹：jdk1.7.0_79

将该文件夹重命名为jdk1.7
命令：
```
mv jdk1.7.0_79/ jdk1.7
```

###1.4 配置环境变量
编辑 /etc/profile文件
命令： vi /etc/profile

在该文件末尾处添加下列内容：
```
export JAVA_HOME=/usr/java/jdk1.7
exportCLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar:$CLASSPATH
export PATH=$JAVA_HOME/bin:$PATH
```
添加完毕后保存。
查看java版本信息：

至此，JDK安装完成。
#2 Tomcat的安装和配置
###2.1 Tomact安装包上传
同JDK上传方法，将tomcat安装包上传至目录 /opt下
###2.2 解压tomcat安装包及项目包上传
命令：tar -xvf apache-tomcat-7.0.69
解压完毕后，/opt目录下

进入apach-tomcat-7.0.69目录下
命令：cd apach-tomcat-7.0.69

将项目文件上传至/opt/apache-tomcat-7.0.69/webapps目录下，将 law_files文件夹上传至 /usr 目录下，上传方法同JDK安装包上传。
##2.3 修改配置信息
###2.3.1 Tomcat默认端口号修改（默认为8080）
路径：/opt/apache-tomcat-7.0.69/conf/server.xml.
```
<Connector port="8181" protocol="HTTP/1.1"
  connectionTimeout="20000"
 redirectPort="8443" URIEncoding='GBK'/>
```


###2.3.2 配置完成后运行startup.sh即可
命令: /opt/apache-tomcat-7.0.69/bin/startup.sh
浏览器中输入网址后出现如下界面，即为安装成功。

###2.3.3 系统时间修改
```
  Date -s 06/20/16 16年06 月20
  Date -s 20:16:25 20时16分25秒
```
###2.3.4 系统配置修改


防止启动tomcat时报错(内存不足)，需添加下列语句。
```
/opt/apache-tomcat-7.0.69/bin/catalina.sh
JAVA_OPTS='-Xms512m -Xmx1024m -XX:MaxPermSize=256m'
```

#附录1 OpenOffice安装
###1.1 上传安装包并解压
上传方法同JDK安装包上传
tar -xvf Apache_OpenOffice_4.1.2_Linux_x86-64_install-rpm_zh-CN.tar.gz
解压完毕后，会在解压目录下出现名为zh-CN的目录
###1.2 安装
进入该目录下的RPMS目录，安装rpm包
命令：rpm -ivh *.rpm
安装完成后，进入该目录下desktop-integration/下

选择相应的操作系统进行安装，该环节为redhat，选在第三个安装
命令：rpm -ivh openoffice4.1.2-redhat-menus-4.1.2-9782.noarch.rpm
至此，openoffice安装完成。
###1.3 启动
进入/opt/openoffice4/program目录下，执行下述语句启动openoffice
soffice -headless -accept="socket,host=127.0.0.1,port=8100;urp;" -nofirststartwizard &
通过netstat –tln可查看端口信息
通过ps –ef | grep soffice可查看运行状况
#附录2 常用Linux命令
cd /usr/java cd 绝对路径，即可进入到相应目录下
mv 移动文件
rm 删除
ll、ls 查看当前目录下所有文件
netstat –tln 查看端口使用信息
tar –xvf 解压tar包
gunzip 解压后缀为gz的包
rpm –ivh 安装rpm包
vi 进入vi编辑器，用来编辑文件，进入后输入i，进入编辑模式，通过光标移动选择修改内容，修改完毕后按Esc后，输入 :wq进行保存。(进行修改文件之前，使用cp *** ***.bak方式备份)
cp 复制





