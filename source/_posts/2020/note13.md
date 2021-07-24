---
title: iOS scrollview 布局
date: 2017-07-19 11:22:29
categories:
- iOS
tags:
- iOS
- scrollview
---

### 当手机界面元素很多的时候，就要滑动界面来查看其他界面元素，此时就要用到 scrollView 组件。

下面介绍了自己在工作中是如何使用 storyborad autolayout 实现 scrollview 的复杂布局。


<!-- more -->

#### 1. 将 Scrollview 拖入视图控制器中，设置 delegate， 添加约束：到四边的距离为 0。


#### 2. 拖入 UIView 命名为 Container 作为容器视图。同样的添加约束：到四边的距离为 0。

#### 3. 拖入 三个 UIView 到 Container 中，分别命名为 TopView， MainView， BottomView。


#### 4. 设置 TopView 约束：宽度等于根视图View的宽度，高度400，到四边的距离为 0. 设置 MainView 约束：高度400，到四边的距离为 0.设置 BottomView 约束：高度400，到四边的距离为 0.

#### 5. 在三个视图中，分别设置自己的布局，完成复杂界面的设计。

>这种布局方法可以完成复杂的界面设计，但是把所有的界面元素都放在了一个 ViewController 中，组件不可重用，修改起来比较麻烦。后期优化可以把可重用的界面分离出来。


