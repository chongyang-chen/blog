---
title: android学习笔记（3-6）
categories:
  - android
tags:
  - android
  - 按钮背景图不显示
date: 2021-02-27 13:46:32
---

android学习笔记。前面学习了四种基本布局，其实还有AbsoluteLayout，TableLayout等，就不一一学习了。等用到了再说。继续学习自定义控件。

<!-- more -->

先看一张图:

<img src="01.png" width=600px>

新建一个UICustonView项目。

<img src="02.png" width=800px>

新建一个layout目录下新家一个title.xml的布局文件。

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:background="@drawable/title_bg">

    <Button
        android:id="@+id/title_back"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_margin="4dp"
        android:background="@drawable/back_bg"
        android:text="Back"
        android:textColor="#fff" />

    <TextView
        android:id="@+id/title_text"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_weight="1"
        android:gravity="center"
        android:text="Title View"
        android:textColor="#fff" />

    <Button
        android:id="@+id/title_edit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center"
        android:layout_margin="4dp"
        android:background="@drawable/edit_bg"
        android:text="Edit"
        android:textColor="#fff" />

</LinearLayout>
```

在 main_activity.xml 引入新创建的布局。

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <include layout="@layout/title" />

</androidx.constraintlayout.widget.ConstraintLayout>
```



运行程序结果如下所示：

<img src="03.png" width=480px>

按钮的背景图片没有显示，设置背景色也没有用。

最后找到了解决方案，在`app/src/main/res/values`目录下有个themes.xml。

修改themes.xml：

```xml
<style name="Theme.UICustomView" 
       parent="Theme.MaterialComponents.DayNight.DarkActionBar.Bridge">
```

程序正常运行：

<img src="04.png" width=480px>



