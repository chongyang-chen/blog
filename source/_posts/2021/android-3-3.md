---
title: android学习笔记（3-3）
categories:
  - android
tags:
  - android
date: 2021-02-27 12:24:35
---

android学习笔记。今天开始4种基本布局的学习。

<!-- more -->

首先看一下布局与控件的关系：

<img src="01.png" width=480px>

通过上面的关系，可以实现一些复杂的界面布局。

### 线性布局

前面的学习都属于线性布局。

新建一个UILayoutTest项目。

<img src="02.png" width=800px>

修改代码如下：

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <Button
        android:id="@+id/button_1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 1" />

    <Button
        android:id="@+id/button_2"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 2" />

    <Button
        android:id="@+id/button_3"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Button 3" />
</LinearLayout>
```

运行结果如下：

<img src="03.png" width=480px>

如果改成水平布局，则是下面的结果：

<img src="04.png" width=480px>

当排列方向为水平时，指定垂直方向的排列方向：

结果如下：

<img src="05.png" width=480px>

同理，当排列方向为垂直时，指定水平方向的排列方向：

<img src="06.png" width=480px>

接下来学习一些实用的布局。