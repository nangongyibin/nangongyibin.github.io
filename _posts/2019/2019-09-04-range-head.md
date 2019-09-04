---
layout: post
title: Range头
category: Html
tags: [Html]
excerpt: Range头
---


## 1、断点下载核心原理 ##

    public static void main(String[] args) {
        try {
            //定义一个访问的路径
            String path = "http://it.nangongyibin.com:8080/resource/a.txt";
            //创建一个url对象，通过url对象访问指定的路径
            URL url = new URL(path);
            //实现敲回车
            HttpURLConnection connection = (HttpURLConnection) url.openConnection();
            //在获取服务器数据之前，要告诉connection对象，获取多少定的数据，通过range头，100代表从100这个位置开始取，-代表一直取完
            connection.setRequestProperty("range", "bytes=100-");
            //获取服务器返回的数据，数据以流的形式返回
            InputStream is = connection.getInputStream();
            //流的对接，把流里面的数据读出来，写到一个文件里
            int len = 0;
            byte[] buf = new byte[1024];
            //创建文件输出流
            FileOutputStream fos = new FileOutputStream("download.txt");
            while ((len = is.read(buf)) != -1) {
                fos.write(buf, 0, len);
            }
            fos.close();
            is.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }