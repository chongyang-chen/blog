---
title: Objective-C 基础教程学习笔记(3)
tags:
  - oc
categories:
  - oc
date: 2016-08-09 18:38:50
---

上节笔记学习了面向对象编程的基础支持，本节学习面向对象的一个重要部分： **继承** 。
<!-- more -->
上节代码有许多重复的地方，把重复的代码提取出来，放到父类中去。子类继承父类，只能继承一个。

> 只有代码精简，代码才无处藏身。

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

@interface Shape : NSObject {
    ShapeColor color;
    ShapeRect bounds;
}

- (void)setColor:(ShapeColor)color;
- (void)setBounds:(ShapeRect)bounds;
- (void)draw;
@end

@implementation Shape

- (void)setColor:(ShapeColor)c {
    color = c;
}
- (void)setBounds:(ShapeRect)b{
    bounds = b;
}
- (void)draw{
}
@end

@interface Circle : Shape
@end

@implementation Circle

- (void)draw{
    NSLog(@"drawing a circle at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

@interface Rectangle : Shape
@end

@implementation Rectangle

- (void)draw{
    NSLog(@"drawing a rectangle at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

@interface Egg : Shape
@end

@implementation Egg

- (void)draw{
    NSLog(@"drawing an egg at (%d %d %d %d) in %@",
          bounds.x, bounds.y, bounds.width, bounds.height, colorName(color));
}
@end

void drawShapes(id shapes[], int count) {
    for (int i = 0; i < count; i++) {
        Shape *shape = shapes[i];
        [shape draw];
    }
}

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
这种优化代码的方式称为重构（refactoring）。通常开发周期包括向代码中添加某些新特性，然后通过重构删除重复的代码。

继承是在两个类之间建立一种关系，可以避免许多重复的代码。复合是对象之间的另一种关系。

以汽车程序为例学习对象的复合，一辆汽车有一个发动机和4个轮子。

```c
#import <Foundation/Foundation.h>

@interface Tire : NSObject
@end

@implementation Tire

- (NSString *)description {
    return @"I am a tire.";
}

@end

@interface Engine : NSObject

@end

@implementation Engine

- (NSString *)description
{
    return @"I am an engine.";
}

@end

@interface Car : NSObject {
    Engine *engine;
    Tire *tires[4];
}
- (void)print;

@end

@implementation Car

- (instancetype)init
{
    self = [super init];
    if (self) {
        engine = [Engine new];
        tires[0] = [Tire new];
        tires[1] = [Tire new];
        tires[2] = [Tire new];
        tires[3] = [Tire new];
    }
    return self;
}

- (void)print {
    NSLog(@"%@", engine);
    NSLog(@"%@", tires[0]);
    NSLog(@"%@", tires[1]);
    NSLog(@"%@", tires[2]);
    NSLog(@"%@", tires[3]);
}
@end
int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Car *car = [[Car alloc] init];
        [car print];
    }
    return 0;
}
```
存取方法，使用存取方法来访问类的实例变量，可以让程序的实现更为灵活，同时也体现了 **封装** 的思想。

```c
#import <Foundation/Foundation.h>

@interface Tire : NSObject
@end

@implementation Tire

- (NSString *)description {
    return @"I am a tire.";
}

@end

@interface Engine : NSObject

@end

@implementation Engine

- (NSString *)description
{
    return @"I am an engine.";
}

@end

@interface Car : NSObject {
    Engine *engine;
    Tire *tires[4];
}

- (Engine *)engine;
- (void)setEngine:(Engine *)newEngine;
- (Tire *)tireEngine:(NSInteger)index;
- (void)setTire:(Tire *)tire atIndex:(NSInteger)index;
- (void)print;

@end

@implementation Car


- (Engine *)engine{
    return engine;
}
- (void)setEngine:(Engine *)newEngine{
    engine = newEngine;
}
- (Tire *)tireEngine:(NSInteger)index{
    return tires[index];
}
- (void)setTire:(Tire *)tire atIndex:(NSInteger)index {
    tires[index] = tire;
}

- (void)print {
    NSLog(@"%@", engine);
    NSLog(@"%@", tires[0]);
    NSLog(@"%@", tires[1]);
    NSLog(@"%@", tires[2]);
    NSLog(@"%@", tires[3]);

}
@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Car *car = [[Car alloc] init];
        Engine *engine = [Engine new];
        [car setEngine:engine];
        for (int i = 0; i < 4; i++) {
            Tire *tire = [Tire new];
            [car setTire:tire atIndex:i];
        }
        [car print];
    }
    return 0;
}
```
Car程序扩展

使用新的发动机和轮子来组装新型号的汽车。

```c
#import <Foundation/Foundation.h>

@interface Tire : NSObject
@end

@implementation Tire

- (NSString *)description {
    return @"I am a tire.";
}

@end

@interface AllWeatherRadial : Tire
@end

@implementation AllWeatherRadial

- (NSString *)description {
    return @"I am a tire for all weather.";
}

@end

@interface Engine : NSObject

@end

@implementation Engine

- (NSString *)description
{
    return @"I am an engine.";
}

@end

@interface Slant6 : Engine

@end

@implementation Slant6

- (NSString *)description {
    return @"I am a slant-6. VROOOM!";
}

@end

@interface Car : NSObject {
    Engine *engine;
    Tire *tires[4];
}

- (Engine *)engine;
- (void)setEngine:(Engine *)newEngine;
- (Tire *)tireEngine:(NSInteger)index;
- (void)setTire:(Tire *)tire atIndex:(NSInteger)index;
- (void)print;

@end

@implementation Car


- (Engine *)engine{
    return engine;
}
- (void)setEngine:(Engine *)newEngine{
    engine = newEngine;
}
- (Tire *)tireEngine:(NSInteger)index{
    return tires[index];
}
- (void)setTire:(Tire *)tire atIndex:(NSInteger)index {
    tires[index] = tire;
}

- (void)print {
    NSLog(@"%@", engine);
    NSLog(@"%@", tires[0]);
    NSLog(@"%@", tires[1]);
    NSLog(@"%@", tires[2]);
    NSLog(@"%@", tires[3]);

}

@end

int main(int argc, const char * argv[]) {
    @autoreleasepool {
        Car *car = [[Car alloc] init];
        Engine *engine = [Slant6 new];
        [car setEngine:engine];
        for (int i = 0; i < 4; i++) {
            Tire *tire = [AllWeatherRadial new];
            [car setTire:tire atIndex:i];
        }
        [car print];
    }
    return 0;
}
```
 继承还是复合  

继承之间建立的关系是"is a"，而复合之间建立的关系是"has a"。比如三角形是一个形状，汽车有一个发动机和四个轮子。
