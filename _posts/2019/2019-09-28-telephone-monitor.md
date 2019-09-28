---
layout: post
title: 电话监听器
category: Service
tags: [Service]
excerpt: 电话监听器
---

## 代码实现步骤   ##


### 开启一个服务 服务在后台监听电话的状态 ###


    public class PhoneService extends Service {
    private static final String TAG = "PhoneService";

	    @Nullable
	    @Override
	    public IBinder onBind(Intent intent) {
	        Log.e(TAG, "onBind: ");
	        return null;
	    }
	
	    @Override
	    public void onStart(Intent intent, int startId) {
	        Log.e(TAG, "onStart: ");
	        super.onStart(intent, startId);
	    }
	
	    @Override
	    public void onCreate() {
	        TelephonyManager tm = (TelephonyManager) getSystemService(TELEPHONY_SERVICE);
	        tm.listen(new MyPhoneStateListener(), PhoneStateListener.LISTEN_CALL_STATE);
	        super.onCreate();
	        Log.e(TAG, "onCreate: ");
	    }
	
	    private class MyPhoneStateListener extends PhoneStateListener {
	
	        private MediaRecorder mRecorder;
	
	        @Override
	        public void onCallStateChanged(int state, String phoneNumber) {
	            switch (state) {
	                case TelephonyManager.CALL_STATE_IDLE://空闲
	                    if (mRecorder != null) {
	                        mRecorder.stop();//停止录音
	                        mRecorder.reset();
	                        mRecorder.release();
	                    }
	                    Log.e(TAG, "onCallStateChanged: CALL_STATE_IDLE");
	                    break;
	                case TelephonyManager.CALL_STATE_RINGING://响铃
	                    mRecorder = new MediaRecorder();
	                    mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);//设置音频来源
	                    mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP);//设置输出文件
	                    mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB);//设置音频编码方式
	                    mRecorder.setOutputFile(Environment.getExternalStorageDirectory().getAbsolutePath()+ File.separator+System.currentTimeMillis()+".mp3");//指定文件的存放路径
	                    try {
	                        mRecorder.prepare();//准备录音
	                    } catch (IOException e) {
	                        e.printStackTrace();
	                    }
	                    Log.e(TAG, "onCallStateChanged: CALL_STATE_RINGING");
	                    break;
	                case TelephonyManager.CALL_STATE_OFFHOOK://通话
	                    if (mRecorder == null) {
	                        mRecorder = new MediaRecorder();
	                        mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);//设置音频来源
	                        mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP);//设置输出文件
	                        mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB);//设置音频编码方式
	                        mRecorder.setOutputFile(Environment.getExternalStorageDirectory().getAbsolutePath()+ File.separator+System.currentTimeMillis()+".mp3");//指定文件的存放路径
	                        try {
	                            mRecorder.prepare();//准备录音
	                        } catch (IOException e) {
	                            e.printStackTrace();
	                        }
	                    }
	                    mRecorder.start();
	                    Log.e(TAG, "onCallStateChanged: CALL_STATE_OFFHOOK");
	                    break;
	            }
	            super.onCallStateChanged(state, phoneNumber);
	        }
	    }
	
	    @Override
	    public int onStartCommand(Intent intent, int flags, int startId) {
	        Log.e(TAG, "onStartCommand: ");
	        return super.onStartCommand(intent, flags, startId);
	    }
	
	    @Override
	    public boolean onUnbind(Intent intent) {
	        Log.e(TAG, "onUnbind: ");
	        return super.onUnbind(intent);
	    }
	
	    @Override
	    public void onDestroy() {
	        Log.e(TAG, "onDestroy: ");
	        super.onDestroy();
	    }
	}


### 具体实现录音功能 ###

    
    private class MyPhoneStateListener extends PhoneStateListener {

        private MediaRecorder mRecorder;

        @Override
        public void onCallStateChanged(int state, String phoneNumber) {
            switch (state) {
                case TelephonyManager.CALL_STATE_IDLE://空闲
                    if (mRecorder != null) {
                        mRecorder.stop();//停止录音
                        mRecorder.reset();
                        mRecorder.release();
                    }
                    Log.e(TAG, "onCallStateChanged: CALL_STATE_IDLE");
                    break;
                case TelephonyManager.CALL_STATE_RINGING://响铃
                    mRecorder = new MediaRecorder();
                    mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);//设置音频来源
                    mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP);//设置输出文件
                    mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB);//设置音频编码方式
                    mRecorder.setOutputFile(Environment.getExternalStorageDirectory().getAbsolutePath()+ File.separator+System.currentTimeMillis()+".mp3");//指定文件的存放路径
                    try {
                        mRecorder.prepare();//准备录音
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                    Log.e(TAG, "onCallStateChanged: CALL_STATE_RINGING");
                    break;
                case TelephonyManager.CALL_STATE_OFFHOOK://通话
                    if (mRecorder == null) {
                        mRecorder = new MediaRecorder();
                        mRecorder.setAudioSource(MediaRecorder.AudioSource.MIC);//设置音频来源
                        mRecorder.setOutputFormat(MediaRecorder.OutputFormat.THREE_GPP);//设置输出文件
                        mRecorder.setAudioEncoder(MediaRecorder.AudioEncoder.AMR_NB);//设置音频编码方式
                        mRecorder.setOutputFile(Environment.getExternalStorageDirectory().getAbsolutePath()+ File.separator+System.currentTimeMillis()+".mp3");//指定文件的存放路径
                        try {
                            mRecorder.prepare();//准备录音
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }
                    mRecorder.start();
                    Log.e(TAG, "onCallStateChanged: CALL_STATE_OFFHOOK");
                    break;
            }
            super.onCallStateChanged(state, phoneNumber);
        }
    }


### 添加对应权限 ###

    
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission android:name="android.permission.RECORD_AUDIO" />

### 出现问题 ###

    at android.media.MediaRecorder.start(Native Method)

解决方案：

setOutputFile必须是绝对路径

