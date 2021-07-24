---
title: Objective-C 基础教程学习笔记(4)
tags:
  - oc
categories:
  - oc
date: 2016-08-10 18:38:50
---

目前为止都是在一个文件中编写代码，实际应该将代码放在 `xx.h ` 和  `xx.m ` 文件中。并通过 `#import` 命令来导入头文件。

`@class` 指令创建了一个前向引用。  <!-- more -->
工具善其事，必先利其器。书中用一个章节的内容专门介绍了 `Xcode` 这个开发工具。书中的版本是4.3.2，现在的版本已经更新到了11.4。界面发生了许多变化。直接开始下一章的学习。

Foundation框架

先看一些有用的数据类型 **NSRange CGPoint CGSize CGRect**，这些数据类型都是C的结构体。

**NSString NSArray NSDictionary NSNumber NSValue NSNull NSData NSDate**这些都是经常用到的类，可以查看API学习具体的使用方法。

查找文件的示例

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        NSFileManager *manager;
        manager = [NSFileManager defaultManager];
        NSString *home;
        home = [@"~" stringByExpandingTildeInPath];
        NSMutableArray *files;
        files = [NSMutableArray arrayWithCapacity:42];
        for (NSString *filename in [manager enumeratorAtPath:home]) {
            if ([[filename pathExtension] isEqualToString:@"pdf"]
                || [[filename pathExtension] isEqualToString:@"mobi"]
                || [[filename pathExtension] isEqualToString:@"epub"]
                ) {
                [files addObject:filename];
            }
        }
        for (NSString *name in files) {
            printf("%s\n", name.UTF8String);
        }
    }
    return 0;
}
```
上面的代码可以帮助你找到电脑中的一些电子书，同理可以查找电脑中的音乐，图片，视频等内容。

内存管理  
内存管理不是一个容易解决的问题。  

对象的生命周期  
程序中对象的生命周期包括诞生，生存，交友，释放。  
内存泄漏（leak memory）：程序的内存占用量不断增加，最终会被耗尽并导致程序崩溃。  
一般笔记本的内存为4G-8G。  
OC使用引用计数来管理对象的声明周期，当对象的引用计数为0，对象将被销毁，占用的内存被系统回收。  
内存管理另一个重要的概念是 **对象所有权**（objective ownership）。

可以将对象放入自动释放池。  
如果使用new，alloc，copy方法获得一个对象，就释放或者自动释放该对象。

垃圾回收，自动内存管理机制。
ARC（automatic reference counting）自动引用计数。  
Xcode新建项目默认开启ARC，使用ARC进行内存管理要避免出现强循环引用。
**__bridge_transfer, __bridge_retained, __bridge** 这是一个标准的C语言类型转换。是一种称为桥接转换（bridge cast）的C语言计数。

异常  
你没有必要让所有人都满意，只需让你在乎的人满意就行了。
