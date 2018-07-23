---
layout:     post
title:      "nginx安装备忘录"
subtitle:   ""
date:       2018-07-23 16:43
author:     "parkin"
header-img: "img/post-bg-js-module.jpg"
catalog: ture
tags:
    - nginx
---
> 小插曲

------
# nginx安装

环境：Ubuntu 18

安装版本：Nginx 1.9.9

安装依赖

安装gcc g++的依赖库

sudo apt-get install build-essential

sudo apt-get install libtool

安装pcre依赖库（http://www.pcre.org/）

sudo apt-get update

sudo apt-get install libpcre3 libpcre3-dev

安装zlib依赖库（http://www.zlib.net）

sudo apt-get install zlib1g-dev

安装SSL依赖库（16.04默认已经安装了）

sudo apt-get install openssl

下载最新版本：

wget http://nginx.org/download/nginx-1.9.9.tar.gz

#解压：

tar -zxvf nginx-1.13.6.tar.gz

#进入解压目录：

cd nginx-1.9.9

#配置：

./configure --prefix=/usr/local/nginx

#编译： make

#安装： sudo make install

#启动： sudo /usr/local/nginx/sbin/nginx

make过程中遇到的问题：



objs/Makefile:445: recipe for target 'objs/src/core/ngx_murmurhash.o' failed

解决方案：将对应的makefile文件夹中（ /nginx-1.9.9/objs/Makefile） 找到 -Werrori 并去掉 在重新make即可

解决方案参考博客：https://blog.csdn.net/qq_36638599/article/details/79424878

