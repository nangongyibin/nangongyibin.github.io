---
layout: post
title: 网页源码查看器
category: NetLib
tags: [NetLib]
excerpt: 网页源码查看器
---


## 代码实现步骤  ##


### [1]搭建UI ###
 
### [2]httpurlconnection类基本用法 ###

    
    public void look(View view) {
        String path = mEt.getText().toString().trim();
        if (!TextUtils.isEmpty(path)) {
            try {
                URL url = new URL(path);
                HttpURLConnection connection = (HttpURLConnection) url.openConnection();
                int code = connection.getResponseCode();
                if (code == 200) {
                    InputStream is = connection.getInputStream();
                    String str = StreamUtils.StreamToString(is);
                    Message message = mHandler.obtainMessage();
                    message.obj = str;
                    mHandler.sendMessage(message);
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }

### [3]把流转换为String工具类 ###

    
    /**
     * @param is
     * @return
     */
    public static String StreamToString(InputStream is) {
        try {
            ByteArrayOutputStream baos = new ByteArrayOutputStream();
            int len = 0;
            byte[] buf = new byte[1024];
            while ((len = is.read(buf)) != -1) {
                baos.write(buf, 0, len);
            }
            return baos.toString();
        } catch (IOException e) {
            e.printStackTrace();
            return "";
        }
    }
    
### [4]联网要加上联网权限 ###

    
    <uses-permission android:name="android.permission.INTERNET" />

当加上权限后，也会报如下错误

android.os.NetworkOnMainThreadException主线程(UI线程)访问网络的异常，主线程这个概念是谷歌提出的。

为什么会报这个异常，谷歌要求在主线程不能进行耗时(拷贝数据 连接网络)的操作，如果在主线程中进行耗时操作会报anr(应用无响应)异常； 如何解决?我们可以自己创建一个线程来访问网络。

### [5]当我们把访问访问的操作放到子线程又会报如下错误: ###

android.view.ViewRootImpl$CalledFromWrongThreadException: Only the original thread that created a view hierarchy can touch its views

只有主线程(UI线程)才可以更新UI

### [6]handler(助手)的使用 —->负责线程的切换  ###

####  6.1创建handler对象   ####

    private Handler mHandler = new Handler() {
        @Override
        public void handleMessage(Message msg) {
            String str = (String) msg.obj;
            mTv.setText(str);
            super.handleMessage(msg);
        }
    };


#### 6.2 发消息 ####

    Message message = mHandler.obtainMessage();
    message.obj = str;
    mHandler.sendMessage(message);



