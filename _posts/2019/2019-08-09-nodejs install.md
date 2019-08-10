---
layout: post
title: nodejs的安装
category: Linux
tags: [Linux]
excerpt: nodejs的安装
---

### 1、安装文件下载 ###

    [http://nodejs.cn/download/](http://nodejs.cn/download/ "下载地址")

### 2、将安装包上传到指定位置(我习惯放到：/usr/local/software/目录)，并解压 ###

    tar -xvf node-v10.6.0-linux-x64.tar.xz

### 3、重命名文件夹 ###

    mv node-v10.6.0-linux-x64 nodejs

### 4、通过建立软连接变为全局 ###

    ln -s /usr/local/software/nodejs/bin/npm /usr/local/bin/
	ln -s /usr/local/software/nodejs/bin/node /usr/local/bin/

### 5、检查是否安装成功，命令：node -v ###

    node -v
	v10.6.0


参考网站：https://www.cnblogs.com/mao2080/p/9346018.html