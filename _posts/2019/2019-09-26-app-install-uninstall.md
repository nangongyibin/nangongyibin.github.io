---
layout: post
title: 应用安装和卸载
category: BroadcastReceiver
tags: [BroadcastReceiver]
excerpt: 应用安装和卸载
---

### 定义广播接收者,用来接收事件(应用安装和卸载的事件) ###

    public class AppReceiver extends BroadcastReceiver {
	    private static final String TAG = "AppReceiver";
	
	    @Override
	    public void onReceive(Context context, Intent intent) {
	        String action = intent.getAction();
	        if (action.equals("android.intent.action.PACKAGE_ADDED")) {
	            Log.e(TAG, "onReceive: 应用安装了");
	        }
	        if (action.equals("android.intent.action.PACKAGE_REMOVED")) {
	            Log.e(TAG, "onReceive: 应用卸载了");
	        }
	    }
	}

### 清单文件配置 ###

    
        <receiver
            android:name=".AppReceiver"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_ADDED" />
                <action android:name="android.intent.action.PACKAGE_REMOVED" />
                <data android:scheme="package" />
            </intent-filter>

        </receiver>

### 但是高API的还需要在代码中进行注册广播接受者 ###

        AppReceiver appReceiver = new AppReceiver();
        IntentFilter intentFilter = new IntentFilter();
        intentFilter.addAction("android.intent.action.PACKAGE_ADDED");
        intentFilter.addAction("android.intent.action.PACKAGE_REMOVED");
        intentFilter.addDataScheme("package");
        registerReceiver(appReceiver,intentFilter);





