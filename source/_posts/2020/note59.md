---
title: Objective-C 基础教程学习笔记(2)
tags:
  - oc
categories:
  - oc
date: 2016-08-08 18:38:50
---

实现面向对象编程  
相关术语
> **类**：表示对象类型的结构体。    
> **对象**：包含值和指向其类的隐藏指针的结构体。  
> **实例**：对象的另一种称呼。  
> **消息**：对象可以执行的操作，用于通知对象去做什么。  
> **方法**：为响应消息而运行的代码。  
> **方法调度**：是OC使用的一种机制，用于推测执行什么方法以响应某个特定的消息。  
> **接口**：类为对象提供的特性描述。  
> **实现**：使接口能正常工作的代码。  
<!-- more -->

过程式编程，首先通过枚举指定几种可以绘制的不同形状。

```c
#import <Foundation/Foundation.h>

typedef enum{
    kCirCle,
    kRectangle,
    kEgg
} ShapeType;

typedef enum {
    kRedColor,
    kGreenColor,
    kBlueColor
} ShapeColor;

typedef struct {
    int x, y, width, height;
} ShapeRect;

typedef struct {
    ShapeType type;
    ShapeColor fillColor;
    ShapeRect bounds;
} Shape;

void drawCircle(ShapeColor color, ShapeRect bounds);
void drawRectangle(ShapeColor color, ShapeRect bounds);
void drawEgg(ShapeColor color, ShapeRect bounds);
NSString * colorName(ShapeColor color);

void drawShapes(Shape *shapes, int count) {
    for (int i = 0; i < count; i++) {
        switch (shapes[i].type) {
            case kCirCle:
                drawCircle(shapes[i].fillColor, shapes[i].bounds);
                break;
                
            case kRectangle:
                drawRectangle(shapes[i].fillColor, shapes[i].bounds);
                break;
                
            case kEgg:
                drawEgg(shapes[i].fillColor, shapes[i].bounds);
                break;
        }
    }
}

void drawCircle(ShapeColor color, ShapeRect bounds) {
    NSLog(@"drawing a circle at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}

void drawRectangle(ShapeColor color, ShapeRect bounds){
    NSLog(@"drawing a rectangle at (%d %d %d %d) in %@",
            bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}

void drawEgg(ShapeColor color, ShapeRect bounds){
    NSLog(@"drawing an egg at (%d %d %d %d) in %@",
            bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}

NSString * colorName(ShapeColor color){
    switch (color) {
        case kRedColor:
            return @"red";
            break;
        case kGreenColor:
            return @"green";
            break;
        case kBlueColor:
            return @"blue";
            break;
    }
}


int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Shape shapes[3];
        ShapeRect rect0 = {0, 0, 10, 30};
        shapes[0].type = kCirCle;
        shapes[0].fillColor = kRedColor;
        shapes[0].bounds = rect0;
        
        ShapeRect rect1 = {30, 40, 50, 60};
        shapes[1].type = kRectangle;
        shapes[1].fillColor = kGreenColor;
        shapes[1].bounds = rect1;
        
        ShapeRect rect2 = {60, 70, 80, 90};
        shapes[2].type = kEgg;
        shapes[2].fillColor = kBlueColor;
        shapes[2].bounds = rect2;
        
        drawShapes(shapes, 3);
        
    }
    return 0;
}
```
上面的代码绘制的圆形，矩形，椭圆形。如果要绘制一个三角形需要修改至少4个不同的位置才能完成该任务。  

面向对象编程 OOP。

```c
#import <Foundation/Foundation.h>

typedef enum {
    kRedColor,
    kGreenColor,
    kBlueColor
} ShapeColor;

typedef struct {
    int x, y, width, height;
} ShapeRect;

void drawShapes(id shapes[], int count) {
    for (int i = 0; i < count; i++) {
        id shape = shapes[i];
        [shape draw];
    }
}

NSString * colorName(ShapeColor color){
    switch (color) {
        case kRedColor:
            return @"red";
            break;
        case kGreenColor:
            return @"green";
            break;
        case kBlueColor:
            return @"blue";
            break;
    }
}


@interface Circle : NSObject {
    @private
    ShapeColor color;
    ShapeRect bounds;
}

- (void)setColor:(ShapeColor)color;
- (void)setBounds:(ShapeRect)bounds;
- (void)draw;
@end

@implementation Circle

- (void)setColor:(ShapeColor)c {
    color = c;
}
- (void)setBounds:(ShapeRect)b{
    bounds = b;
}
- (void)draw{
    NSLog(@"drawing a circle at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

@interface Rectangle : NSObject {
    @private
    ShapeColor color;
    ShapeRect bounds;
}

- (void)setColor:(ShapeColor)color;
- (void)setBounds:(ShapeRect)bounds;
- (void)draw;
@end

@implementation Rectangle

- (void)setColor:(ShapeColor)c {
    color = c;
}
- (void)setBounds:(ShapeRect)b{
    bounds = b;
}
- (void)draw{
    NSLog(@"drawing a rectangle at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

@interface Egg : NSObject {
    @private
    ShapeColor color;
    ShapeRect bounds;
}

- (void)setColor:(ShapeColor)color;
- (void)setBounds:(ShapeRect)bounds;
- (void)draw;
@end

@implementation Egg

- (void)setColor:(ShapeColor)c {
    color = c;
}
- (void)setBounds:(ShapeRect)b{
    bounds = b;
}
- (void)draw{
    NSLog(@"drawing an egg at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        id shapes[3];
        ShapeRect rect0 = {0, 0, 10, 30};
        shapes[0] = [Circle new];
        [shapes[0] setBounds:rect0];
        [shapes[0] setColor:kRedColor];
        
        ShapeRect rect1 = {30, 40, 50, 60};
        shapes[1] = [Rectangle new];
        [shapes[1] setBounds:rect1];
        [shapes[1] setColor:kGreenColor];
        
        ShapeRect rect2 = {60, 70, 80, 90};
        shapes[2] = [Egg new];
        [shapes[2] setBounds:rect2];
        [shapes[2] setColor:kBlueColor];
       
        drawShapes(shapes, 3);
        
    }
    return 0;
}
```
运行上面的代码需要将设置项目 **Automatic Reference Counting**  变为No。使用面向对象可以方便的添加绘制三角形的功能。  
> **开放/关闭原则**：软件实体应该对扩展开放，对修改关闭。  

遵循开放/关闭原则的软件，应对变化时，不必修改那些可以正常运行的代码。

复制粘贴容易出现大量重复的代码。应该编写更少的代码来完成工作。


