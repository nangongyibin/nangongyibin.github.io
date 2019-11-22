---
layout: post
title:    照相和录像   
category: Other
tags: [Other]
excerpt:  照相和录像  
---


三星、小米、华为、魅族……深圳:华强北，7: 7000


    public void playPhoto(View view) {
        Intent intent = new Intent(MediaStore.ACTION_IMAGE_CAPTURE);
        File file = new File(getFilesDir().getPath(), "1.png");
        Uri uri = Uri.fromFile(file);
        intent.putExtra(MediaStore.EXTRA_OUTPUT,uri);
        startActivityForResult(intent,7219);
    }

    public void playVideo(View view) {
        Intent intent = new Intent(MediaStore.ACTION_VIDEO_CAPTURE);
        File file = new File(getFilesDir().getPath(), "2.3pg");
        Uri uri = Uri.fromFile(file);
        intent.putExtra(MediaStore.EXTRA_OUTPUT,uri);
        startActivityForResult(intent,9127);
    }

