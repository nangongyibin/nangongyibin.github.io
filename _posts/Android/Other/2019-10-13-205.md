---
layout: post
title:    播放视频  
category: Other
tags: [Other]
excerpt:  播放视频 
---


## 播放音频和播放视频区别:播放视频有一个画面:—->SurfaceView  ##

## 代码实现过程 ##

### 在布局声明 ###

    <SurfaceView
        android:id="@+id/sfv"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

### surface控件特点: 属于一个重量级控件，初始化需要点时间，通过声明周期来完成视频播放 ###

    private void initSfv() {
        mSfv = findViewById(R.id.sfv);
        SurfaceHolder holder = mSfv.getHolder();
        holder.addCallback(new SurfaceHolder.Callback() {

            private MediaPlayer mMediaPlayer;
            private int currentPosition;
            @Override
            public void surfaceCreated(SurfaceHolder holder) {
                try {
                    mMediaPlayer = new MediaPlayer();
                    mMediaPlayer.setDataSource("http://it.nangongyibin.com:8080/resource/cc.mp4");
                    mMediaPlayer.prepareAsync();
                    mMediaPlayer.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
                        @Override
                        public void onPrepared(MediaPlayer mp) {
                            mp.start();
                            mp.seekTo(currentPosition);
                        }
                    });
                } catch (IOException e) {
                    e.printStackTrace();
                }
            }

            @Override
            public void surfaceChanged(SurfaceHolder holder, int format, int width, int height) {
                if (mSfv!=null && mMediaPlayer.isPlaying()){
                    currentPosition = mMediaPlayer.getCurrentPosition();
                    mMediaPlayer.stop();
                }
            }

            @Override
            public void surfaceDestroyed(SurfaceHolder holder) {

            }
        });
    }



mediaplayer播放视频，格式只支持3gp、mp4。

### VideoView ###

    private void initVideoView() {
        try {
            mVv = findViewById(R.id.vv);
            mVv.setVideoPath("http://it.nangongyibin.com:8080/resource/cc.mp4");
            mVv.start();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

