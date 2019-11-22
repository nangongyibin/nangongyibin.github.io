---
layout: post
title:    fragment生命周期  
category: Fragment
tags: [Fragment]
excerpt:  fragment生命周期 
---


在实际开发中，只需要重写onCreateView 和 onDestroy方法就可够用了，在onCreateView方法里面初始化控件，在ondestroy方法里面做扫尾的工作，比如解绑服务、释放资源。