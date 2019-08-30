---
layout: post
title: Module-build详解
category: Other
tags: [Other]
excerpt: Module-build详解
---

    apply plugin: 'com.android.application'

	android {
	    compileSdkVersion 28
        buildToolsVersion "28.0.3"
	    defaultConfig {
	        applicationId "com.ngyb.test"
	        minSdkVersion 15
	        targetSdkVersion 28
	        versionCode 1
	        versionName "1.0"
	        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
	    }
	    buildTypes {
	        release {
	            minifyEnabled false
	            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt'), 'proguard-rules.pro'
	        }
	    }
	}
	
	dependencies {
	    implementation fileTree(dir: 'libs', include: ['*.jar'])
	    implementation 'com.android.support:appcompat-v7:28.0.0'
	    implementation 'com.android.support.constraint:constraint-layout:1.1.3'
	    testImplementation 'junit:junit:4.12'
	    androidTestImplementation 'com.android.support.test:runner:1.0.2'
	    androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.2'
	}


## 1）apply plugin ##

主要有两种选中选择：

### com.android.application表示应用程序模块 ###

### com.android.library表示库模块 ###

## 2）android闭包 ##

### ①、compileSdkVersion用来指定项目的编译版本 ###

### ②、buildToolsVersion用于项目构建工具的版本 ###

### ③、defaultConfig闭包 ###

applicationId用于指定项目的包名

minSdkVersion用于指定项目最低兼容的Android系统版本

targetSdkVersion指定的值表示在该版本做过充分测试

versionCode用于指定项目的版本号

versionName用于指定项目的版本名

### ④、buildTypes闭包 ###

通常只会有两个子闭包，一个是debug闭包，一个是release闭包

minifyEnabled用于指定是否对项目代码进行混淆

proguardFiles用于指定混小时使用的规则文件。proguard-android-optimize.txt是所有项目通用的混淆规则；proguard-rules.pro是当前项目特有的混淆规则。


## 3）dependencies闭包 ##

implementation fileTree本地依赖声明，表示将lib下的.jar文件添加到项目的构建路径当中

implementation远程依赖库格式

testImplementation用于声明测试用例库



