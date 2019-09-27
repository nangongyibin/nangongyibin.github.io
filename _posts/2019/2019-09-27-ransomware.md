---
layout: post
title: 勒索软件
category: BroadcastReceiver
tags: [BroadcastReceiver]
excerpt: 勒索软件
---

### 定义广播接收者,接收手机重启事件 ###

    public class RandwareReceiver extends BroadcastReceiver {
	    @Override
	    public void onReceive(Context context, Intent intent) {
	        Intent intent1 = new Intent(context, MainActivity.class);
	        intent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK);
	        context.startActivity(intent);
	    }
	}

### 清单文件配置 ###

    
        <receiver android:name=".RandwareReceiver"
            android:exported="true"
            android:enabled="true">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED"/>
            </intent-filter>
        </receiver>







