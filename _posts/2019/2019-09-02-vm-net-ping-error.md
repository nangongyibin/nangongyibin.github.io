---
layout: post
title: 关于VMware虚拟机网络ping不通外网问题
category: Linux
tags: [Linux]
excerpt: 关于VMware虚拟机网络ping不通外网问题
---

## 1、修改服务器的网络配置文件 ##

![](http://www.nangongyibin.com/assets/images/vnpe1.png)

## 2、打开windows服务管理，启动所有关于VMware的相关服务，在重新打开VMware，并启动虚拟机 ##

![](http://www.nangongyibin.com/assets/images/vnpe2.png)

并输入命令

![](http://www.nangongyibin.com/assets/images/vnpe3.png)

说明已经可以连接外网了。

注意：如果是拷贝别人的虚拟机那么你操作系统分配给VMware的ip、与箭头所指不一致，这时候你就要设置一下箭头所指的ip地址要与Windows系统的一致。

![](http://www.nangongyibin.com/assets/images/vnpe4.png)

打开cmd命令输入ipconfig 查看相关ip地址

![](http://www.nangongyibin.com/assets/images/vnpe5.png)

参考网址：

<https://blog.csdn.net/tap_into/article/details/79676680>


