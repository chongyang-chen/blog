---
title: android学习笔记（3-2）
categories:
  - android
tags:
  - android
date: 2021-02-27 11:45:25
---

android学习笔记。今天开始ProgressBar的学习。

<!-- more -->

### ProgressBar

代码如下：

```xml
<ProgressBar
    android:id="@+id/progress_bar"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    style="?android:attr/progressBarStyleHorizontal"
    android:max="100"/>
```

运行程序，结果如下：

<img src="01.png" width=480px>

### AlertDialog

对话框代码如下：

```java
AlertDialog.Builder dialog = new AlertDialog.Builder(this);
dialog.setTitle("这是一个对话框！");
dialog.setMessage("一些重要信息！");
dialog.setCancelable(false);
dialog.setPositiveButton("确定", (dialog12, which) -> {

});
dialog.setNegativeButton("取消", (dialog1, which) -> {

});
dialog.show();
```

运行效果如下：

<img src="02.png" width=480px>

### ProgressDialog

代码如下：

```java
ProgressDialog progressDialog = new ProgressDialog(this);
progressDialog.setTitle("This is a ProgressDialog!");
progressDialog.setMessage("Loading...");
progressDialog.setCancelable(true);
progressDialog.show();
```

编译器提示下面信息：

<img src="03.png" width=600px>

<img src="05.png" width=800px>

现实效果如下：

<img src="04.png" width=480px>

先不用管他，继续后面的学习。