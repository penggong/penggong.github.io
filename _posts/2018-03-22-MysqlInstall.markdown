---
layout:     post
title:      "mysql安装小插曲"
subtitle:   ""
date:       2018-03-22 15:08
author:     "parkin"
header-img: "img/mysql.jpg"
catalog: ture
tags:
    - mysql
---
> 小插曲

------


# 一、Visual Studio 2013 Redistributable 安装完成后仍提示安装

问题描述：如小标题

环境：windows serve 2008

安装包：官网下载5.7msi包,使用rar离线包因为本地缺少文件必须使用安装包版，

历程：Visual Studio 2013 Redistributable 安装完成后仍提示安装，经查因为操作系统为中文，mysql 提供的visul是英文版的，mysql匹配时就会出现异常，可以手动下载安装中文版，-_-

# 二、 远程连接授权

## 2.1 出入站端口加入
## 2.2 远程连接用户授权

```
grant all privileges on *.* to 'test'@'%'identified by '123456' with grant option;
```

## 2.3linux 还需要查看 mysql配置文件，默认的3306，有可能会默认配置了
bind-address = 127.0.0.1  


