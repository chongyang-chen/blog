---
title: flutter 初探
categories:
  - flutter
tags:
  - flutter
date: 2021-03-19 10:46:59
---

今天来学习一下flutter，网上也有很多关于flutter的教程，今天主要通过flutter中文网来学习。

<!-- more -->

我的设备：

<img src="01.png" width=560px>

首先是flutter的安装与环境配置，整个过程没有遇到大的问题。

```bash
cc@ccy ~ % flutter --version
Flutter 2.0.2 • channel stable • https://github.com/flutter/flutter.git
Framework • revision 8962f6dc68 (7 days ago) • 2021-03-11 13:22:20 -0800
Engine • revision 5d8bf811b3
Tools • Dart 2.12.1
cc@ccy ~ % flutter doctor   
Doctor summary (to see all details, run flutter doctor -v):
[✓] Flutter (Channel stable, 2.0.2, on macOS 11.2.3 20D91 darwin-arm, locale
    zh-Hans-CN)
[✓] Android toolchain - develop for Android devices (Android SDK version 30.0.3)
[✓] Xcode - develop for iOS and macOS
[✓] Chrome - develop for the web
[✓] Android Studio (version 4.1)
[✓] IntelliJ IDEA Community Edition (version 2020.3.3)
[✓] Connected device (3 available)
• No issues found!
cc@ccy ~ %
```

编译工具的设定，使用 Android Studio 安装 flutter 插件，新建一个Flutter App。

打开Android Studio选择新建Flutter项目，

<img src="02.png" width=660px>

输入Package name，选中 iOS和Android 平台，点击Finish完成创建。

<img src="03.png" width=660px>

项目结构如下：

<img src="04.png" width=460px>

包含了iOS和android连个项目。

选择模拟器或者真机运行项目：

<img src="05.png" width=460px>

iOS真机：

<img src="06.png" width=360px>

iOS模拟器：

<img src="07.png" width=360px>

android真机：

<img src="08.png" width=360px>

以上就是Flutter的开发体验初探，Flutter使用一套代码可以开发web，iOS和Android三个平台的软件。看上去十分的高大上，就是运行的时候有点慢，需要等待一段时间，真机测试的时候也会遇到一些问题，接下来继续学习flutter。