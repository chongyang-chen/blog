---
title: 《Objective-C高级编程》学习笔记（2）
categories:
  - Objective-C
tags:
  - Objective-C
  - Blocks
date: 2021-03-01 18:56:45
---

《Objective-C高级编程》学习笔记。第二章 Blocks 。

<!-- more -->

Blocks 是C语言的扩充功能，是带有自动变量的匿名函数。能够编写不带名称的函数对程序员来说相当具有吸引力。

Blocks语法与C语言函数定义相比，仅有两点不同：

1. 没有函数名；
2. 带有“^”。

Blocks可以进行简化，省略返回值和参数列表。

Blocks类型变量与一般的C语言变量完全相同。

使用typedef来简化Blocks类型定义。

__block 说明符，实现在Block内赋值。

Blocks的实质，使用 `clang -rewrite-objc`将含有Blocks语法的源代码变换为C++源代码，其实也仅仅是使用了struct结构，其本质还是C语言源代码。

### Block循环引用

如果在Block中使用附有 __strong 修饰符的对象类型自动变量，那么当Block从栈复制到堆时，该对象为Block所持有，这样容易引起循环引用。

