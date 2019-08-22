---
layout: post
title: Activity启动模式
category: Activity
tags: [Activity]
excerpt: Activity启动模式
---

standard：标准，默认是这个启动模式，打开一个页面进栈，关闭一个页面出栈。

singleTop：单一顶部，当activity配置成这个启动模式，当开启这个页面的时候，系统会检查任务栈栈顶是否已经有该实例存在，如果有直接复用；如果没有，重新创建一个实例进栈。

singleTask：当页面配置成这个启动模式的时候，当开启这个页面的时候，系统就会检查整个任务栈是否有实例存在，如果有直接复用，并且还会把这个实例上面其他的实例清空。

singleInstance：当页面配置这个启动模式，当开启这个页面的时候，系统会为这个页面创建一个新的任务栈，并且这个任务栈里面只有这一个实例存在。