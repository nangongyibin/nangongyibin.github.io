---
layout: post
title:    播放音乐逻辑 
category: Other
tags: [Other]
excerpt:  播放音乐逻辑 
---

## mediaplayer 播放音频和视频 ##


        try {
            String path = Environment.getExternalStorageDirectory().getPath() + "/data/xpg.mp3";
            Log.e(TAG, "Play: " + path);
            mMediaPlayer.setDataSource(path);
            mMediaPlayer.prepare();
            mMediaPlayer.start();
            Toast.makeText(this, "播放", Toast.LENGTH_SHORT).show();
            updataProgress();
        } catch (IOException e) {
            e.printStackTrace();
        }


## 完善百度音乐盒,为了提升音乐播放器案例进程优先级,所以我们把播放的逻辑写到服务里  ##

### 完善UI 加上一个进度条 代表播放歌曲的进度 ###

	<?xml version="1.0" encoding="utf-8"?>
	<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:orientation="vertical"
	    tools:context=".MainActivity">
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click1"
	        android:text="start开启服务" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click2"
	        android:text="start关闭服务" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click3"
	        android:text="bind开启服务" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click4"
	        android:text="bind关闭服务" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click5"
	        android:text="开启屏幕的服务" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="Certificate"
	        android:text="办证" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click6"
	        android:text="开始播放" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click7"
	        android:text="暂停播放" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click8"
	        android:text="继续播放" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click9"
	        android:text="AIDL测试" />
	
	    <Button
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:onClick="click10"
	        android:text="买豆" />
	
	    <SeekBar
	        android:id="@+id/sb"
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content" />
	</LinearLayout>

### 实现播放歌曲、暂停、继续播放的逻辑 ###

    public void Play() {
        try {
            String path = Environment.getExternalStorageDirectory().getPath() + "/data/xpg.mp3";
            Log.e(TAG, "Play: " + path);
            mMediaPlayer.setDataSource(path);
            mMediaPlayer.prepare();
            mMediaPlayer.start();
            Toast.makeText(this, "播放", Toast.LENGTH_SHORT).show();
            updataProgress();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

### 暂停歌曲 ###

    public void Pause() {
        mMediaPlayer.pause();
        Toast.makeText(this, "暂停", Toast.LENGTH_SHORT).show();
    }

### 继续播放歌曲 ###


    public void ContinuePlay() {
        mMediaPlayer.start();
        Toast.makeText(this, "继续播放", Toast.LENGTH_SHORT).show();
    }

### 实现更新进度条的逻辑: ###

    private void updataProgress() {
        final Timer timer = new Timer();
        TimerTask timerTask = new TimerTask() {
            @Override
            public void run() {
                int duration = mMediaPlayer.getDuration();
                int currentPosition = mMediaPlayer.getCurrentPosition();
                Bundle bundle = new Bundle();
                bundle.putInt("max",duration);
                bundle.putInt("current",currentPosition);
                Message obtain = Message.obtain();
                obtain.setData(bundle);
                MainActivity.mHandler.sendMessage(obtain);
            }
        };
        timer.schedule(timerTask,1000,1000);
        mMediaPlayer.setOnCompletionListener(new MediaPlayer.OnCompletionListener() {
            @Override
            public void onCompletion(MediaPlayer mp) {
                timer.cancel();
            }
        });
    }

#

    @SuppressLint("HandlerLeak")
    public static Handler mHandler = new Handler(){
        @Override
        public void handleMessage(Message msg) {
            super.handleMessage(msg);
            Bundle data = msg.getData();
            int max = data.getInt("max");
            int current = data.getInt("current");
            mSb.setMax(max);
            mSb.setProgress(current);
        }
    };

### 实现拖拽进度条,播放歌曲指定位置.首先在服务内部暴漏一个方法,用来播放歌曲指定位置。 ###

    private void PlayPosition(int position) {
        mMediaPlayer.seekTo(position);
    }

### 给进度条设置一个监听 当拖动停止的时候播放歌曲的指定位置: ###

        mSb.setOnSeekBarChangeListener(new SeekBar.OnSeekBarChangeListener() {
            @Override
            public void onProgressChanged(SeekBar seekBar, int progress, boolean fromUser) {
                
            }

            @Override
            public void onStartTrackingTouch(SeekBar seekBar) {

            }

            @Override
            public void onStopTrackingTouch(SeekBar seekBar) {
                mMusicServer.playPosition(seekBar.getProgress());
            }
        });


### 当歌曲播放完成了，取消tiemr(计时器) ###

        mMediaPlayer.setOnCompletionListener(new MediaPlayer.OnCompletionListener() {
            @Override
            public void onCompletion(MediaPlayer mp) {
                timer.cancel();
            }
        });

### 播放网络音频代码 ###

    public void net(View view) {
        new Thread(new Runnable() {
            @Override
            public void run() {
                try {
                    MediaPlayer mediaPlayer = new MediaPlayer();
                    mediaPlayer.setDataSource("http://it.nangongyibin.com:8080/resource/xpg.mp3");
                    mediaPlayer.prepareAsync();
                    mediaPlayer.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
                        @Override
                        public void onPrepared(MediaPlayer mp) {
                            Log.e(TAG, "onPrepared: 准备好了" );
                            mp.start();
                        }
                    });
                } catch (IOException e) {
                    Log.e(TAG, "run: "+e.getLocalizedMessage() );
                    e.printStackTrace();
                }
            }
        }).start();
    }

