---
title: 《Objective-C高级编程》学习笔记（1）
categories:
  - Objective-C
tags:
  - Objective-C
date: 2021-03-01 18:56:32
---

《Objective-C高级编程》学习笔记。今天开始学习第一章的内容，自动引用计数。

<!-- more -->

<img src="01.png" width=320px>

首先要了解引用计数，办公室开灯的例子很好的解释了引用计数问题。

### 内存管理的思考方式

1. 自己生成的对象，自己持有。

2. 非自己生成的对象，自己也能持有。

3. 不需要自己持有的对象时释放。

4. 非自己持有的对象无法释放。

接着分析了内存管理的实现。GNUstep源码分析。

区域，NSZone为了防止内存碎片化而引入的结构。使用多重区域可以防止内存碎片化。

但是，运行时系统中的内存管理本身已极具效率，使用区域反而会引起内存使用效率低下以及源代码复杂化等问题。

苹果的实现，利用xcode的调试器lldb和iOS大概分析其实现过程。 苹果的实现大概是采用散列表（引用计数表）来管理引用计数。通过引用计数表来管理引用计数有如下好处：

1. 对象的内存块分配无需考虑内存块头部。
2. 引用计数表各记录中存有内存块地址，可从各个记录追溯到各对象的内存块。
3. 检测内存泄漏时，引用计数表的各记录也有助于检测各对象的持有者是否存在。

autorelease 类似于C语言中的自动变量的特性。 

大量产生autorelease对象时，只要不废弃NSAutoreleasePool, 生成的对象就不能被释放，有时会产生内存不足的现象。

提高调用Objective-C方法的速度，一种被称为 **IMP Caching** 的技术，一般而言速度是其他方法的2倍。

如果autorelease NSAutoreleasePool对象会如何？会发生异常。

### ARC规则

同一个程序中可以按文件单位选择ARC有效/无效。

所有权修饰符：

1. __strong 修饰符

2. __weak 修饰符

3. __unsafe_unretained 修饰符

4. __autoreleasing 修饰符

__strong 是默认的修饰符，

__weak 弱引用，用于解决循环用于问题，对象被废弃时，将被设置为nil，只能用于iOS 5 以上版本的应用。

赋值给 __unsafe_unretained 变量的对象在通过该变量使用时，如果没有确保其确实存在，那么程序就会崩溃。

Objective-C对象和Core Foundation对象。

Core Foundation对象主要使用在用C语言编写的Core Foundation框架中，并使用引用计数的对象。

__bridge 转换，id型或对象型变量赋值给void *或者逆向赋值时都需要进行特定的转换。

__brigde_retained : 可使要转换赋值的变量也持有所赋值的对象。

__bridge_transfer :被转换的变量所持有的对象在该变量被赋值给转换目标变量后随之释放。

属性声明的属性与所有权修饰符的对应关系：

| 属性声明的属性    | 所有权修饰符        |
| :---------------- | ------------------- |
| copy              | strong              |
| retain            | strong              |
| strong            | strong              |
| unsafe_unretained | __unsafe_unretained |
| weak              | __weak              |
| assign            | __unsafe_unretained |

