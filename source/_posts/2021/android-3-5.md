---
title: android学习笔记（3-5）
categories:
  - android
tags:
  - android
date: 2021-02-27 13:46:28
---

android学习笔记。今天开始学习其他布局方式。

<!-- more -->

### 帧布局

应用场景较少，默认摆放在左上角的布局方式。

### 百分比布局

修改build.gradle。

```json
dependencies {
    implementation 'androidx.appcompat:appcompat:1.1.0'
    implementation 'androidx.percentlayout:percentlayout:1.0.0'
    implementation 'com.google.android.material:material:1.1.0'
    implementation 'androidx.constraintlayout:constraintlayout:1.1.3'
    testImplementation 'junit:junit:4.13.2'
    androidTestImplementation 'androidx.test.ext:junit:1.1.1'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.2.0'
}
```

添加百分比布局：

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.percentlayout.widget.PercentFrameLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <Button
        android:id="@+id/button1"
        android:text="Button1"
        android:layout_gravity="left|top"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:layout_height="0dp"
        android:layout_width="0dp"
        tools:ignore="RtlHardcoded" />

    <Button
        android:id="@+id/button2"
        android:text="Button2"
        android:layout_gravity="right|top"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:layout_height="0dp"
        android:layout_width="0dp"
        tools:ignore="RtlHardcoded" />

    <Button
        android:id="@+id/button3"
        android:text="Button3"
        android:layout_gravity="left|bottom"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:layout_height="0dp"
        android:layout_width="0dp"
        tools:ignore="RtlHardcoded" />

    <Button
        android:id="@+id/button4"
        android:text="Button4"
        android:layout_gravity="right|bottom"
        app:layout_widthPercent="50%"
        app:layout_heightPercent="50%"
        android:layout_height="0dp"
        android:layout_width="0dp"
        tools:ignore="RtlHardcoded" />
</androidx.percentlayout.widget.PercentFrameLayout>
```



效果如下：

<img src="01.png" width=480px>

垂直方向有间隙，水平方向是紧挨着的。使用的代码和书中有所不同，上面这种方法也已经不被推荐了 deprecated。

最新的布局方式是constraintlayout，被称作约束布局。新建项目使用的就是这种布局方式。

```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
```

这些知识要以后慢慢学习，先来学习书中后面的内容。

