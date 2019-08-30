---
layout: post
title: SharedPreferences
category: Other
tags: [Other]
excerpt: SharedPreferences
---

SharedPreferences偏爱 喜爱

## sp基本使用步骤 ##


    mSp = getSharedPreferences("Config", 0);
	boolean isCheck = mSp.getBoolean("是否记录密码", false);
	//保存是否记住密码
    mSp.edit().putBoolean("是否记录密码", checked).apply();
