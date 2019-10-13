---
layout: post
title:    动态添加fragment   
category: Fragment
tags: [Fragment]
excerpt:  动态添加fragment  
---

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        WindowManager wm = (WindowManager) getSystemService(WINDOW_SERVICE);
        Display display = wm.getDefaultDisplay();
        int width = display.getWidth();
        int height = display.getHeight();
        FragmentManager fm = getSupportFragmentManager();
        if (width > height){
            fm.beginTransaction().replace(R.id.content,new OneFragment()).commit();
        }else{
            fm.beginTransaction().replace(R.id.content,new TwoFragment()).commit();
        }
    }


通过v4包中的fragment支持低版本。

兼容低版本就是使用V4包中的fragment。

注意地方:在获取fragm管理者的方式不一样了

	FragmentManager fm = getSupportFragmentManager();