---
layout: post
title:   mysql安装出现error Nr.1045  
category: MySql
tags: [MySql]
excerpt:  mysql安装出现error Nr.1045
---

## 1.管理工具---服务里面停止MySQL服务。（在运行里输入”services.msc”，回车） ##

## 2.控制面板---卸载Mysql，删除C:\Program Files\MySQL目录 ##

## 3.这是最关键一步，只做前面两步，密码还是修改不了，因为MySQL 还有文件，也就是在C:\Documents and Settings\All Users\Application Data里面的MySQL文件夹（或者删除C:\Documents and Settings\All Users下的Application Data）。 ##

这个文件没有清除是MySQL重装出现旧密码的根源所在，于是删除MySQL文件夹

## 4.检查C:\WINDOWS目录下是否有my.ini文件,将其删 ##

## 5.注册表里的HEKY_LOCAL_MACHINE，SOFTWARE，MYSQL删除（在运行里输入”regedit”，回车） ##

       HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Services\Eventlog\Application\MySQL 目录删除　　HKEY_LOCAL_MACHINE\SYSTEM\ControlSet002\Services\Eventlog\Application\MySQL 目录删除       HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Eventlog\Application\MySQL 目录删除完成以上步骤，就可以重新安装MySQL并且进行全新配置了（注意是全新配置）


参考网址：

<https://jingyan.baidu.com/article/e52e36157a97c740c60c51f7.html>

