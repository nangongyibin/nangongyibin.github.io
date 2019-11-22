---
layout: post
title: 注册特殊广播接收者
category: Service
tags: [Service]
excerpt: 注册特殊广播接收者
---


    public class ScreenService extends Service {
    	private SpecialRadioReceiver mSpecialRadioReceiver;

	    @Nullable
	    @Override
	    public IBinder onBind(Intent intent) {
	        return null;
	    }
	
	    @Override
	    public void onCreate() {
	        mSpecialRadioReceiver = new SpecialRadioReceiver();
	        IntentFilter intentFilter = new IntentFilter();
	        intentFilter.addAction("android.intent.action.SCREEN_ON");
	        intentFilter.addAction("android.intent.action.SCREEN_OFF");
	        registerReceiver(mSpecialRadioReceiver, intentFilter);
	        super.onCreate();
	    }
	
	    @Override
	    public void onDestroy() {
	        unregisterReceiver(mSpecialRadioReceiver);
	        super.onDestroy();
	    }
	}