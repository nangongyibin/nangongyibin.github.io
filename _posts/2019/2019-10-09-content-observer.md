---
layout: post
title:    通过内容提供者向联系人数据库插入联系人
category: ContentProvider
tags: [ContentProvider]
excerpt:  通过内容提供者向联系人数据库插入联系人 
---

- 内容观察者不是四大组件，可以用来观察数据库是否被操作了
- 注册内容观察者代码如下:

-
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Uri uri = Uri.parse("content://ngyb.ltz/insert");
        getContentResolver().registerContentObserver(uri, true, new ContentObserver(new Handler()) {
            @Override
            public void onChange(boolean selfChange, Uri uri) {
                super.onChange(selfChange, uri);
                Log.e(TAG, "onChange: 执行内容观察者");
            }
        });
    }