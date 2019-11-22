---
layout: post
title: 图片查看器
category: NetLib
tags: [NetLib]
excerpt: 图片查看器
---


## 和源码查看器区别: ##
	1 UI不一样
	2 数据展示的方式不一样
	3  访问路径的不一样

## runOnUIthread ##

    						runOnUiThread(new Runnable() {
                                @Override
                                public void run() {
                                   mIv.setImageBitmap(bitmap);
                                }
                            });

## bitmapFactory  位图工厂 ##

	final Bitmap bitmap = BitmapFactory.decodeStream(is);