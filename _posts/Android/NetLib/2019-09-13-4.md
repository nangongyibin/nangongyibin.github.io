---
layout: post
title: AsyncHttpClient 
category: NetLib
tags: [NetLib]
excerpt: AsyncHttpClient 
---

## get:提交代码 ##

    
    public void AsyncHttpClientGet() {
        String username = mUsername.getText().toString().trim();
        String password = mPassword.getText().toString().trim();
        String path = "http://192.168.0.103:8080/login/loginServlet?username=" + username + "&&password=" + password;
        AsyncHttpClient client = new AsyncHttpClient();
        client.get(path, new AsyncHttpResponseHandler() {
            @Override
            public void onSuccess(int statusCode, Header[] headers, byte[] responseBody) {
                showToast(new String(responseBody));
            }

            @Override
            public void onFailure(int statusCode, Header[] headers, byte[] responseBody, Throwable error) {
                Log.e(TAG, "onFailure: " + error.toString() + "===" + statusCode);
            }
        });
    }

## post:提交代码实现 ##

    
    public void AsyncHttpClientPost() {
        String username = mUsername.getText().toString().trim();
        String password = mPassword.getText().toString().trim();
        String path = "http://192.168.0.103:8080/login/loginServlet";
        AsyncHttpClient client = new AsyncHttpClient();
        RequestParams params = new RequestParams();
        params.add("username", username);
        params.add("password", password);
        client.post(path, params, new AsyncHttpResponseHandler() {
            @Override
            public void onSuccess(int statusCode, Header[] headers, byte[] responseBody) {
                showToast(new String(responseBody));
            }

            @Override
            public void onFailure(int statusCode, Header[] headers, byte[] responseBody, Throwable error) {
                Log.e(TAG, "onFailure: " + error.toString() + "===" + statusCode);
            }
        });
    }