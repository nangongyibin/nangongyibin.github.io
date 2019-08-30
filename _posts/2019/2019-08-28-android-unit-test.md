---
layout: post
title: Android中的单元测试
category: Other
tags: [Other]
excerpt: Android中的单元测试
---

## 1、测试的分类  ##

### 1.1根据是否知道源代码：黑盒(不知道源码)、白盒(需要知道源代码) ###

### 1.2根据测试粒度：方法、单元、系统、集成 ###

### 1.3根据测试的暴力程度：压力(12306)、冒烟、谷歌提供了一个工具(monkey) ###

## 2、单元测试 想在测试的方法上面加上一个@Test符号 ##

    public class ExampleUnitTest {
	    @Test
	    public void addition_isCorrect() {
	        assertEquals(4, 2 + 2);
	    }
	}