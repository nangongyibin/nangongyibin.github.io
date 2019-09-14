---
layout: post
title: AndroidManifest
category: Other
tags: [Other]
excerpt: AndroidManifest
---
# 1、manifest #

package指定程序的报名

## 1、application闭包 ##



如果想让你的应用程序有多个启动入口应该做如下配置:


    <activity android:name=".MainActivity">
            <intent-filter>
                <action android:name="android.intent.action.MAIN" />

                <category android:name="android.intent.category.LAUNCHER" />
            </intent-filter>
    </activity>


### 1.1、activity闭包 ###

application节点下的icon和label可以和activity节点下不一样，如果activity自己配置了icon和label属性使用自己的。

android:name来指定具体注册哪一个活动

android：label指定活动中标题栏的内容

#### 1.1.1.1、intent-filter ####

###### action #####

 android:name

###### category #####

 android:name











