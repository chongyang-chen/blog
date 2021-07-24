---
title: String与NSString的区别
categories:
  - swift
tags:
  - swift
  - NSString
date: 2021-03-05 18:11:25
---

Swift 的String类型与 Foundation NSString类进行了无缝桥接。在日常开发中，绝大多数应该用 String 。
<!-- more -->
String 与 NSString 还有以下区别

1. String类型是值类型(不再是对象类型)，字符串在进行常量、变量赋值操作或在函数/方法中传递时，会进行值拷贝。 任何情况下，都会对已有字符串值创建新副本，并对该新副本进行传递或赋值操作。
2. String 可以支持字符遍历NSString 不支持。
3. String 是一个结构体，性能更高；NSString 是一个 NSObject 对象，性能相对会差。
4. 现在还有一些功能，用 String 不方便实现： 取字符串的字串/判断包含/正则表达式。