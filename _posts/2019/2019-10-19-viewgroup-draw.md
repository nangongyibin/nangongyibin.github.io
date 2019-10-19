---
layout: post
title:    viewGroup绘制流程  
category: Layout
tags: [Layout]
excerpt:  viewGroup绘制流程
---


总结：当继承ViewGroup的时候必须要重写onMeasure方法和onLayout方法，在onMeasure方法里面完成对孩子的测量，在onLayout方法里面完成对孩子的摆放。
 
当继承View的时候必须要重写onMeasure方法和onDraw方法，在onMeasure方法里面完成对当前view的测量，在onDraw完成绘制。
