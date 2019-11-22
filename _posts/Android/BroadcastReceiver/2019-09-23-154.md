---
layout: post
title: 短信监听器
category: BroadcastReceiver
tags: [BroadcastReceiver]
excerpt: 短信监听器
---

### 定义广播接收者,接收发送的短信 ###

    public class SmsReceiver extends BroadcastReceiver {
	    private static final String TAG = "SmsReceiver";
	
	    @Override
	    public void onReceive(Context context, Intent intent) {
	        Object[] pdus = (Object[]) intent.getExtras().get("pdus");
	        for (Object pdu : pdus) {
	            SmsMessage smsMessage = SmsMessage.createFromPdu((byte[]) pdu);
	            String body = smsMessage.getMessageBody();
	            String address = smsMessage.getOriginatingAddress();
	            Log.e(TAG, "onReceive: " + address + "====" + body);
	        }
	    }
	}

### 在清单文件注册广播接收者 ###

    <receiver
        android:name=".SMSreceiver"
        android:enabled="true"
        android:exported="true">
        <intent-filter>
            <action android:name="android.provider.Telephony.SMS_RECEIVED" />
        </intent-filter>
    </receiver>

### 但是高API的需要在代码中进行注册广播接受者 ###

        SmsReceiver myReceiver = new SmsReceiver();
        IntentFilter filter = new IntentFilter();
        filter.addAction("android.provider.Telephony.SMS_RECEIVED");
        registerReceiver(myReceiver, filter);





