---
layout: post
title: HttpClient 
category: NetLib
tags: [NetLib]
excerpt: HttpClient 
---

# Httpclient实现get和post提交 #


## 代码实现过程  ##


导包 implementation 'com.loopj.android:android-async-http:1.4.9' 把这个包导入到build.gradle里 


httlclient实现get提交数据

    
    public void HttpClientGet() {
        try {
            String username = mUsername.getText().toString().trim();
            String password = mPassword.getText().toString().trim();
            String path = "http://192.168.0.103:8080/login/loginServlet?username=" + username + "&&password=" + password;
            HttpGet httpGet = new HttpGet(path);
            HttpClient client = new DefaultHttpClient();
            HttpResponse res = client.execute(httpGet);
            InputStream stream = res.getEntity().getContent();
            String s = StreamUtils.StreamToString(stream);
            showToast(s);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

使用httpclient实现post提交

    
    public void HttpClientPost() {
        try {
            String username = mUsername.getText().toString().trim();
            String password = mPassword.getText().toString().trim();
            String path = "http://192.168.0.103:8080/login/loginServlet";
            HttpClient client = new DefaultHttpClient();
            HttpPost httpPost = new HttpPost(path);
            List<BasicNameValuePair> pairs = new ArrayList<>();
            BasicNameValuePair pair1 = new BasicNameValuePair("username", username);
            BasicNameValuePair pair2 = new BasicNameValuePair("password", password);
            pairs.add(pair1);
            pairs.add(pair2);
            UrlEncodedFormEntity entity = new UrlEncodedFormEntity(pairs);
            httpPost.setEntity(entity);
            HttpResponse response = client.execute(httpPost);
            InputStream content = response.getEntity().getContent();
            String s = StreamUtils.StreamToString(content);
            showToast(s);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }