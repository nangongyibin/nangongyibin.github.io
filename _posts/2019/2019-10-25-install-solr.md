---
layout: post
title:    Linux部署Solr服务  
category: Linux
tags: [Linux]
excerpt:  Linux部署Solr服务
---

## 1.将solr压缩包上传到web项目-solr文件夹下 ##

![](http://www.nangongyibin.com/assets/images/is1.png)

## 2.解压solr-5.5.4.zip到当前文件夹下 ##

linux 解压zip文件到当前目录 unzip filename.zip

![](http://www.nangongyibin.com/assets/images/is2.png)

![](http://www.nangongyibin.com/assets/images/is3.png)

提示没有unzip 在线安装 继续执行解压缩命令

![](http://www.nangongyibin.com/assets/images/is4.png)

解压成功后 可以看到 solr-5.5.4文件夹

## 3.进入solr-5.5.4/bin尝试启动solr ##

![](http://www.nangongyibin.com/assets/images/is5.png)

启动失败 提示没有权限 linux添加权限

添加权限命令：chmod a+x 文件名

![](http://www.nangongyibin.com/assets/images/is6.png)

看到 绿了说明权限添加成功

## 4. 启动solr命令 ./solr start 启动成功 可以访问以下8983端口 ##

停止solr命令 ./solr stop

![](http://www.nangongyibin.com/assets/images/is7.png)

参考网址：

<https://blog.csdn.net/ggrjake25/article/details/86537850>