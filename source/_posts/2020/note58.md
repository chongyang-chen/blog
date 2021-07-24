---
title: Objective-C 基础教程学习笔记(1)
tags:
  - oc
categories:
  - oc
date: 2016-08-07 18:38:50
---
刚学习 iOS 的时候买了本Objective-C 基础教程的书籍，现在已经过去了5年了，iOS 系统都更新到了13了，重新翻开这本书，记录自己的学习笔记。
<!-- more -->

[《Objective-C基础教程（第2版）》](https://www.ituring.com.cn/book/1129)

操作系统：
![](http://ccyit.cn/images/01.png)

Xcode版本：
![](http://ccyit.cn/images/02.png)

新建一个简单的程序：

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        // insert code here...
        NSLog(@"Hello, World!");
    }
    return 0;
}
```

布尔类型

OC 的布尔类型是 BOOL ，具有 YES 和 NO 两个值。  
下面是使用布尔类型的简单程序。

```c
#import <Foundation/Foundation.h>

//判断两个数是否不同
BOOL areIntsDifferent(int n1, int n2) {
    return n1 == n2 ? NO : YES;
}

//返回字符串
NSString *boolString(BOOL yesNo) {
    return yesNo == NO ? @"NO" : @"YES";
}

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        BOOL areTheyDifferent;
        areTheyDifferent = areIntsDifferent(5, 5);
        NSLog(@"Are %d and %d different? %@", 5, 5, boolString(areTheyDifferent));
        areTheyDifferent = areIntsDifferent(23, 42);
        NSLog(@"Are %d and %d different? %@", 23, 42, boolString(areTheyDifferent));
    }
    return 0;
}
```

面向对象编程-OOP（Object-Oriented Programming）。

变量与间接：

>**只要再多一层间接，计算机科学中就没有解决不了的问题。**

下面的代码计算了从1到10的整数和。

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"The sum from 1 to 10:");
        int sum = 0;
        for (int i = 1; i <= 10; i++) {
            sum += i;
        }
        NSLog(@"%d", sum);
    }
    return 0;
}
```
修改上面的代码计算1到100的和。

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        NSLog(@"The sum from 1 to 100:");
        int sum = 0;
        for (int i = 1; i <= 100; i++) {
            sum += i;
        }
        NSLog(@"%d", sum);
    }
    return 0;
}
```
需要把代码中的10改为100，改动的地方为两处。可以添加一个变量 `count`，解决这个问题。

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        int count = 10000;
        NSLog(@"The sum from 1 to %d:", count);
        int sum = 0;
        for (int i = 1; i <= count; i++) {
            sum += i;
        }
        NSLog(@"%d", sum);
    }
    return 0;
}
```

使用文件名的链接。

```c
#import <Foundation/Foundation.h>

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        const char *filename = "words.txt";
        int bufferLength = 80;

        FILE *file = fopen(filename, "r");
        char word[bufferLength];
        while (fgets(word, bufferLength, file)) {
            word[strlen(word) - 1] = '\0';
            NSLog(@"%s is %lu characters long", word, strlen(word));
        }
        fclose(file);
    }
    return 0;
}
```

面向对象编程中使用间接。  


