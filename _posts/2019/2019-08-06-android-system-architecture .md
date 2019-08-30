---
layout: post
title: Android系统架构
category: Other
tags: [Other]
excerpt: Android系统架构
---

Android大致分为4层架构：Linux内核层、系统运行库层、应用框架层、应用层。

### Linux内核层 ###

Linux内核层主要为Android设备的各种硬件提供底层驱动。

### 系统运行库层 ###

系统运行库层主要通过C/C++库为Android设备提供特性支持。 

系统运行库层还包括运行时库，为Android设备提供技术支持。Android运行时库还包括Dalvik虚拟机（5.0系统之后改为ART运行环境），使得每一个运行程序都运行在一个独立的进程当中，并且拥有一个自己的Dalvik虚拟机实例。、

### 应用框架层 ###

应用框架层为构建应用程序提供了各种API。


### 应用层 ###

手机上的安装的每一个应用程序都属于这一层。