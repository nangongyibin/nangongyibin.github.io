---
layout: post
title: 文件上传案例
category: Java
tags: [Java]
excerpt: 文件上传案例
---

## 背景 ##

朋友圈，邮箱上传附件，百度云盘，360云盘。
 
## 代码实现过程： ##

### 客户端要求： ###

	要求form表单必须有一个文件上传项 
	请求的方式必须为post 因为get提交数据有大小的限制 
	必须加上一个enctype = multipart/form-data 否则请求体里面没有内容

### 服务器逻辑: ###

    
    @GetMapping(value = "upload")
    public void uploadFile(HttpServletRequest request) throws IOException, ServletException {
        request.setCharacterEncoding("utf-8");
        Part part = request.getPart("file");
        String header = part.getHeader("Content-Disposition");
        System.out.println(header);
        String[] split = header.split(";");
        String file = split[split.length - 1];
        String[] filename = file.split("=");
        String str = filename[filename.length - 1];
        String fn = str.substring(1, str.length() - 1);
        String path = ClassUtils.getDefaultClassLoader().getResource("").getPath();
        System.out.println(path);
        System.out.println(fn);
        part.write(path+fn);
    }