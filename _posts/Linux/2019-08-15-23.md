---
layout: post
title: Centos6忘记密码的拯救办法
category: Linux
tags: [Linux]
excerpt: Centos6忘记密码的拯救办法
---

## 1、开机按esc ##

![](http://www.nangongyibin.com/assets/images/centos23.png)

## 2、按 e 键进入编辑模式 ##

选择Kernel /vmlinz-2.6.32-696.e16... ... 后按 e 键编辑此项  

![](http://www.nangongyibin.com/assets/images/centos24.png)

![](http://www.nangongyibin.com/assets/images/centos25.png)

## 3、进入该编辑模式后，在quiet后面输入 simple 或者 1 然后回车     ##

![](http://www.nangongyibin.com/assets/images/centos26.png)

## 4、按 b 键进入单用户模式 ##

passwd root

输入2次新密码  

![](http://www.nangongyibin.com/assets/images/centos27.png)

## 5、reboot  重启  ##

![](http://www.nangongyibin.com/assets/images/centos28.png)