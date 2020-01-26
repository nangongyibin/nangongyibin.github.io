---
layout: post
title:    内容提供者------数据库
category: ContentProvider
tags: [ContentProvider]
excerpt:  内容提供者------数据库
---

- 在应用1的内部定义一个内容提供者 
	- URI:统一资源标示符 也表示一个路径 这个路径可以自己定义
	- URL:统一资源定位符 www.baidu.com

- 在内容提供者内部定义一个urimatcher 并且定义一个静态代码块添加匹配规则 

-

	private static UriMatcher mUriMatcher = new UriMatcher(UriMatcher.NO_MATCH);
    private MyOpenHelper mMyOpenHelper;
    private static int INSERT_SUCCESS = 12;
    private static int DELETE_SUCCESS = 13;
    private static int UPDATE_SUCCESS = 14;
    private static int QUERY_SUCCESS = 15;

    static {
        mUriMatcher.addURI("ngyb.ltz", "insert", INSERT_SUCCESS);
        mUriMatcher.addURI("ngyb.ltz", "delete", DELETE_SUCCESS);
        mUriMatcher.addURI("ngyb.ltz", "update", UPDATE_SUCCESS);
        mUriMatcher.addURI("ngyb.ltz", "query", QUERY_SUCCESS);
    } 


- 把增删改查方法暴漏出去

-


	    @androidx.annotation.Nullable
	    @Override
	    public Cursor query(@androidx.annotation.NonNull Uri uri, @androidx.annotation.Nullable String[] projection,
	                        @androidx.annotation.Nullable String selection, @androidx.annotation.Nullable String[] selectionArgs,
	                        @androidx.annotation.Nullable String sortOrder) {
	        int code = mUriMatcher.match(uri);
	        if (code == QUERY_SUCCESS) {
	            SQLiteDatabase db = mMyOpenHelper.getWritableDatabase();
	            Cursor user = db.query("user", projection, selection, selectionArgs, null, null, null);
	            getContext().getContentResolver().notifyChange(uri, null);
	            return user;
	        } else {
	            throw new IllegalArgumentException("路径错误");
	        }
	
	//        return null;
	    }


- 其他应用程序提供内容解析者操作数据库

-

		Uri uri = Uri.parse("content://ngyb.ltz/query");
        Cursor cursor = getContentResolver().query(uri, null, null, null, null);
        if (cursor != null) {
            while (cursor.moveToNext()) {
                Log.e(TAG, "query: " + cursor.getInt(0) + "==" + cursor.getString(1) + "==" + cursor.getString(2) + "==" + cursor.getString(3));
            }
            cursor.close();
        }



