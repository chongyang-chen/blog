---
title: iOS 设计模式实践
date: 2018-01-29 20:49:52
tags:
- iOS
- 设计模式
categories:
- iOS
---


[原文地址:https://www.raywenderlich.com/46988/ios-design-patterns](https://www.raywenderlich.com/46988/ios-design-patterns)

iOS设计模式——你可能通过这个术语，但是你知道它究竟是什么吗？虽然程序员们认为设计模式是非常重要的，但是并没有很多关于设计模式的文章，并且当我们敲代码的时，很多时候并没有过多的去注意它们。

<!-- more -->
在软件开发中设计模式被用来解决一些常见的问题。
他们是模板，可以帮助你写出那些容易理解和可重用的代码，也可以帮助你创建松耦合的代码，使你不需要太多的麻烦就可以在你的代码中修改或者替换你的组件。

如果你是设计模式新手，那么我有一个好消息给你！首先，多亏了Cocoa自身包含了许多设计模式，所以你已经使用了许多iOS设计模式，鼓励你去使用它们是最好的实践。其次，这个教程将会带着你去掌握所有主要的（和不是那么主要的）iOS设计模式，这些设计模式在Cocoa中被经常使用。

这个教程分为多个部分，一个部分一个设计模式。在每个部分中，你将会读到下面的一个例子：

1. 这个设计模式是什么。
2. 为什么我应该使用它。
3. 怎么使用它，以及什么地方只用它，当使用它时要小心的常见陷阱。

在这个教程中你将会创建一个音乐专辑app，这个app可以展示你的唱片集合和它们的相关信息。

在开发app的整个过程中，你将会掌握以下最最常用的Cocoa设计模式：

1. Creational：单例和抽象工厂。
2. Structural：MVC，装饰者，适配器，外观，符合。
3. Behavioral：观察者，备忘录，责任者链，命令。

不要被误导认为这是一篇纯理论的文章，你将在你的音乐app中使用许多这些设计模式，学完整个教程你的app将会是下面这个样子：

![0.png](http://upload-images.jianshu.io/upload_images/2353580-2befb47194819c75.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


我们开始吧！

下载[starter project](https://koenig-media.raywenderlich.com/uploads/2013/07/BlueLibrary-Starter.zip)，解压zip文件，使用Xcode打开项目文件 *BlueLibrary.xcodeproj* 。

开始的项目并没有太多的内容，仅仅默认的 ViewController 和一个没有实现的简单的HTTP客户端。

>注意：你知道吗？一旦你创建了一个新的Xcode项目，你的代码中就已经使用了设计模式。MVC，代理，协议，单例——你是免费得到他们的哦！

在你沉浸在第一个设计模式之前，你必须创建链各个类去存储和展示唱片集数据。

使用"File\New\File..."(或者使用快捷键 Command+N)。选择iOS>Cocoa Touch 然后选择Objective-C class 点击Next。设置类的名子是Album，父类是NSObject，点击Next，然后点击Create。

打开Album.h 在@interface和@end之间添加下面的属性和方法声明：

```

@property (nonatomic, copy, readonly) NSString *title, *artist, *genre, *coverUrl, *year;

- (id)initWithTitle:(NSString*)title artist:(NSString*)artist coverUrl:(NSString*)coverUrl year:(NSString*)year;

```
标记所有属性是 **readonly**，是因为当Album对象创建后，没有必要去改变他们。

对象的初始化方法，当你创建一个新的album，你将要传递name，artist，cover URL和year。

打开Album.m在@implementation和@end之间加入以下代码：

```
- (id)initWithTitle:(NSString*)title artist:(NSString*)artist coverUrl:(NSString*)coverUrl year:(NSString*)year
{
    self = [super init];
    if (self)
    {
        _title = title;
        _artist = artist;
        _coverUrl = coverUrl;
        _year = year;
        _genre = @"Pop";
    }
    return self;
}

```

到现在并没有神奇的地方，仅仅是一个简单的初始化方法去创建新的Album实例。

再来，使用 File\New\File... 选择Cocoa Touch然后选择 Objective-C class点击Next，设置类的名字是AlbumView，但是这次设置父类是 UIView，点击Next然后Create。

>注意：如果你觉得使用快捷键更方便， **Command+N** 是新建文件， **Command+Option+N** 是新建一个组， **Command+B** 是编译项目， **Command+R** 是运行项目。


打开AlbumView.h 在@interface和@end之间添加下面代码：

```
- (id)initWithFrame:(CGRect)frame albumCover:(NSString*)albumCover;
```

现在打开AlbumView.m 在@implementation后面用下面的代码替换所有代码。

```
@implementation AlbumView
{
    UIImageView *coverImage;
    UIActivityIndicatorView *indicator;
}

- (id)initWithFrame:(CGRect)frame albumCover:(NSString*)albumCover
{
    self = [super initWithFrame:frame];
    if (self)
    {

        self.backgroundColor = [UIColor blackColor];
        // the coverImage has a 5 pixels margin from its frame
        coverImage = [[UIImageView alloc] initWithFrame:CGRectMake(5, 5, frame.size.width-10, frame.size.height-10)];
        [self addSubview:coverImage];

        indicator = [[UIActivityIndicatorView alloc] init];
        indicator.center = self.center;
        indicator.activityIndicatorViewStyle = UIActivityIndicatorViewStyleWhiteLarge;
        [indicator startAnimating];
        [self addSubview:indicator];
    }
    return self;
}

@end
```

你注意到第一件事这里有一个名为coverImage的实例变量，这个变量用于展示专辑的封面图片，第二个变量是一个 indicator，当图片正在下载时，它旋转着表明程序正常运行。

在初始化方法的实现中设置背景颜色为黑色，创建的imageview 有5个像素的边距，创建并添加活动指示器。

>注意：好奇想知道为什么私有变量被定义在实现文件中，而不是接口文件中吗？这是因为在AlbumView类的外面没有类需要知道这些变量的存在，他们仅在类的内部方法的实现中被使用。如果你创建一个库（library）或者框架（framework）给其他的程序员去使用，那么这个约定是非常特别及其重要的。

编译你的项目( **Command+B** ),确保一切井然有序。都好了吗？
那么准备好你的第一个设计模式来了！:]

# MVC——设计模式之王

![mvcking.png](http://upload-images.jianshu.io/upload_images/2353580-f042ee092e5d1889.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

模型 视图 控制器(MVC)是Cocoa的众多设计模式中的一个，并且毫无疑问的是所有设计模式中使用最多的设计模式之一。在你的应用中根据角色给对象分类，根据角色拆分代码，使代码更整洁，条理清晰。

这三种角色分别是：

1. 模型：控制你的应用的数据以及定义如何操作数据。例如，在你的应用中模型是Album类。

2. 视图：控制模型的视觉表现以及用户的交互行为；基本上，所有的UIViews以及他们的子类都属于视图。在你的应用中AlbumView属于视图。

3. 控制器：协调所有工作的中间者，它从模型中获取数据然后将数据在视图上展示，在必要的时候监听事件，并且操作数据。你能够猜到哪个类是你的控制器吗？没错，就是：ViewController。

在你的应用中这个设计模式的好的实现意味着每个对象都有属于自己的组。

下图很好的描述了在模型和视图之间通过控制器进行交流：

![mvc0.png](http://upload-images.jianshu.io/upload_images/2353580-463aeb0f485bc28c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


模型通知控制器数据的改变，相反的，控制器在视图里更新改变后的数据。

视图可以通知控制器用户执行的动作，控制器根据需要更新模型或者重新获取请求的数据。

你可能好奇为什么不能丢弃控制器，在一个类里实现模型和视图，这样看起来更简单点。

所有这一切都是为了代码分离和可重用性。理想上，视图应该完全和模型分离，如果视图不依赖于一个特殊的模型的实现，那么他就可以用于不通的模型，展示一些其他的数据。

例如，如果未来你也想要添加电影或者书籍，你可以仍然使用AlbumView来展示你的电影和书籍对象。此外，如果你想创建一个新的项目，其中有一些与albums有关，你可以简单的重用你的Album类，因为它和任何视图都无关。这就是MVC的魔力。

## 怎么使用MVC模式

首先，你需要确保在你的项目里每一个类都可以划分到模型，视图，控制器中的一个。不要在一个类里包含两种不同的角色。到目前为止你已经完成了一个好的开始，创建了一个Album类和一个AlbumView类。

然后，为了确保你按照这个方法工作，应该创建三个项目组管理你的代码，一个对应一个角色。

使用File\New\Group(或者快捷键Command+Option+N)
命名为Model，重复相同的过程创建View和Controller组。

现在拖拽Album.h和Album.m到Model组，拖拽AlbumView.h和AlbumView.m到View组，最后拖拽ViewController.h和ViewController.m到Controller组。

在这里点上项目目录结构应该看起来像下面这样：

![mvc1.png](http://upload-images.jianshu.io/upload_images/2353580-218f692e794b4c7c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


没有了那些杂乱无序的文件你的工程已经开起来好很多了。当然了，你可以有其他的分组和类，但是应用的核心是包含在这三个组中。

现在你的组件是有组织的了，你需要从某个地方得到唱片集数据。你将要创建一个API类，通过你的代码管理这些数据——这正好给出了一个讨论你的下一个设计模式的机会——单例。

# 单例模式

单例设计模式确保对于一个给定的类只存在一个实例，有一个全局的路径指向这个实例。当第一次需要时通常使用懒加载来创建单例。

>注意：Apple使用了许多单例。例如[NSUserDefaults standardUserDefaults], [UIApplication sharedApplication], [UIScreen mainScreen], [NSFileManager defaultManager] 都返回一个单例对象。

你可能想知道为什么你这么的在意一个类会存在多于一个实例。代码和内存都是便宜的，对不对？

一些情况在一个类有且仅有一个实例是有重要意义的。例如，不需要更多的Logger实例，除非你想要一次写几个日志文件。或者，获得一个全局的配置管理类：实现线程安全的访问一个单独的共享资源，例如一个配置文件，要比许多对象可能同时修改这个配置文件要简单的多得多。

## 怎么使用单例模式

来看一看下面的图表：

![singleton.png](http://upload-images.jianshu.io/upload_images/2353580-4c6a027c4dbc45a0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


上图展示了一个Logger类，有一个单独的属性（是一个单独的实例），和两个方法 sharedInstance 和init。

第一次一个客户端发送sharedInstance消息，instance属性还没有称初始化，因此你创建了这个类的一个新的实例并且返回它的引用。

下一次你调用sharedInstance，instance不需要初始化马上返回，这个逻辑保证了一直都是只有一个实例存在。

你将要通过创建一个单例类管理所有的唱片集数据来实现这个模式。

你注意到了在项目里有一个名为API的组，这里面放了为你的app提供服务的所有类。在这个组里使用 **iOS\Cocoa Touch\Objective-C class** 模板创建一个新的类,名字为LibraryAPI，父类为NSObject。
打开LibraryAPI.h,用下面的代码替换它的内容：

```
@interface LibraryAPI : NSObject

+ (LibraryAPI*)sharedInstance;

@end
```

现在去LibraryAPI.m,在@implementation这一行的后面插入下面的方法：

```
+ (LibraryAPI*)sharedInstance
{
    // 1
    static LibraryAPI *_sharedInstance = nil;

    // 2
    static dispatch_once_t oncePredicate;

    // 3
    dispatch_once(&oncePredicate, ^{
        _sharedInstance = [[LibraryAPI alloc] init];
    });
    return _sharedInstance;
}
```
在这个短短的方法里发生了许多事情：

1. 声明了一个静态变量来持有类的实例，确保在类中实例一直是有效的。
2. 声明静态变量 dispatch_once_t ，确保初始化代码仅执行一次。
3. 使用 Grand Central Dispatch(GCD)执行语句块，实例化一个LibraryAPI的实例。单例设计模式的实质：一旦一个类已经实例化，就再也不会被再次的调用。

下一次你调用sharedInstance方法，在dispatch_once块里面的代码将不会执行(因为已经执行过一次了)，你得到的是之前创建的LibraryAPI实例的引用。

>注意：想要学习更多的关于GCD的知识，请在我们的网站查看教程[Multithreading and Grand Central Dispatch](https://www.raywenderlich.com/?p=4295)和[How to Use Blocks](https://www.raywenderlich.com/?p=9328)

现在你有了单例对象来管理唱片集，更进一步的创建一个类控制数据的持久化存储。

使用 **iOS\Cocoa Touch\Objective-C class** 模板在API组里创建一个新类，命名为PersistencyManager，父类NSObject。

打开PersistencyManager.h,在文件头部添加下面的import语句：

```
#import "Album.h"
```
接下来，在PersistencyManager.h文件@interface这行的后面添加下面的代码：

```
- (NSArray*)getAlbums;
- (void)addAlbum:(Album*)album atIndex:(int)index;
- (void)deleteAlbumAtIndex:(int)index;
```

上面是你需要操作Album数据的三个方法的声明。

打开PersistencyManager.m文件在@implementation后面添加下面的代码：

```
@interface PersistencyManager () {
    // an array of all albums
    NSMutableArray *albums;
}
```
上面的代码添加了一个类的扩展，这是另一个为类添加私有方法和变量的途径，外部的类将不会知道它们。在这，你定义了一个可变数组去存储album数据，使添加和删除数据变得容易许多。

现在在PersistencyManager.m文件@implementation后面添加下面的代码：

```
- (id)init
{
    self = [super init];
    if (self) {
    	// a dummy list of albums
        albums = [NSMutableArray arrayWithArray:
                 @[[[Album alloc] initWithTitle:@"Best of Bowie" artist:@"David Bowie" coverUrl:@"http://www.coversproject.com/static/thumbs/album/album_david%20bowie_best%20of%20bowie.png" year:@"1992"],
                 [[Album alloc] initWithTitle:@"It's My Life" artist:@"No Doubt" coverUrl:@"http://www.coversproject.com/static/thumbs/album/album_no%20doubt_its%20my%20life%20%20bathwater.png" year:@"2003"],
                 [[Album alloc] initWithTitle:@"Nothing Like The Sun" artist:@"Sting" coverUrl:@"http://www.coversproject.com/static/thumbs/album/album_sting_nothing%20like%20the%20sun.png" year:@"1999"],
                 [[Album alloc] initWithTitle:@"Staring at the Sun" artist:@"U2" coverUrl:@"http://www.coversproject.com/static/thumbs/album/album_u2_staring%20at%20the%20sun.png" year:@"2000"],
                 [[Album alloc] initWithTitle:@"American Pie" artist:@"Madonna" coverUrl:@"http://www.coversproject.com/static/thumbs/album/album_madonna_american%20pie.png" year:@"2000"]]];
    }
    return self;
}

```

在init中你用5个例子albums填充了数组，如果上面的唱片集不是你喜欢的，用你喜欢的音乐替换他们是一件很酷的事情。:]

现在添加下面三个方法到PersistencyManager.m中去。

```
- (NSArray*)getAlbums
{
    return albums;
}

- (void)addAlbum:(Album*)album atIndex:(int)index
{
    if (albums.count >= index)
    	[albums insertObject:album atIndex:index];
    else
    	[albums addObject:album];
}

- (void)deleteAlbumAtIndex:(int)index
{
    [albums removeObjectAtIndex:index];
}

```

这些方法允许你获取，添加和删除albums。

编译你的项目确保一切事情顺利进行。

在这一部分，你可能想知道为什么要有PersistencyManager这个类，它并不是一个单例呀。PersistencyManager和LibraryAPI之间的关系将会在下一个章节揭秘，在那里你将会看到外观设计模式。

#外观设计模式

![facade.jpg](http://upload-images.jianshu.io/upload_images/2353580-6ee65630137933f8.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


外观设计模式为一个复杂的子系统提供一个单一的接口。你只需要暴漏一个简单地统一的API，取代向用户暴漏一组类和它们的APIs。

下图解释了这个概念：

![design1.png](http://upload-images.jianshu.io/upload_images/2353580-e5350d9aa4ba8c8d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


API的使用者完全不知道下层的复杂程度。当处理大量的类，特别是使用这些类起来很复杂或者特别难理解的时候，使用外观设计模式是理想的选择。


外观设计模式将使用系统的代码进行解耦，将类的接口和实现对你隐藏，在子系统的内部工作中减少了对外部代码的依赖，外观下面的类可能会修改，当改变发生在幕后时外观仍旧保持相同的API。

例如，如果有一天你想要替换你的后台服务，你不需要改变使用你PAI的代码，因为他们将不会改变。

一般的，你有PersistencyManager保存album数据到本地，并且HTTPClient用来操控远程交流，在你的项目里的其他的类不应该知道这些逻辑。

为了实现这个模式，LibraryAPI仅仅需要持有PersistencyManager和HTTPClient的实例。

然后，LibraryAPI需要提供一些简单的API来访问这些服务。

>注意：通常，一个单例存在app的整个生命周期。你不应该在单例中持有太多的对象的强引用，因为它们直到app关闭才会被释放。

这个设计看起来像下面的样子：

![design2.png](http://upload-images.jianshu.io/upload_images/2353580-edac20b1f9cd350e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


LibraryAPI将会暴漏给其他的代码，但是将会隐藏HTTPClient和PersistencyManager的复杂部分。

打开LibraryAPI.h 在文件顶部添加import语句：

```
#import "Album.h"
```

然后，添加下面的方法定义到LibraryAPI.h中

```
- (NSArray*)getAlbums;
- (void)addAlbum:(Album*)album atIndex:(int)index;
- (void)deleteAlbumAtIndex:(int)index;
```

到现在，你将会暴漏这些方法给其他的类。

去LibraryAPI.m文件，添加下面的两条import语句：

```
#import "PersistencyManager.h"
#import "HTTPClient.h"
```
这是唯一的引入这些类的地方。记住了:你的API将会是访问你的"复杂"系统的唯一的途径。

现在，通过类的扩展添加一些私有变量(在@implementation这行的上面)：

```
@interface LibraryAPI () {
    PersistencyManager *persistencyManager;
    HTTPClient *httpClient;
    BOOL isOnline;
}

@end
```

isOnline 决定了任何的album数据的修改是否应该更新服务，例如添加或者删除数据。

你现在应该通过init方法初始化这些变量，添加下面的代码到LibraryAPI.h中：

```
- (id)init
{
    self = [super init];
    if (self) {
        persistencyManager = [[PersistencyManager alloc] init];
        httpClient = [[HTTPClient alloc] init];
        isOnline = NO;
    }
    return self;
}
```

HTTP 客户端不会真正的与一个服务器工作，这里只是用来展示外观模式的使用，所以isOnline总是NO。:]

接下来，添加下面三个方法到LibraryAPI.m

```
- (NSArray*)getAlbums
{
    return [persistencyManager getAlbums];
}

- (void)addAlbum:(Album*)album atIndex:(int)index
{
    [persistencyManager addAlbum:album atIndex:index];
    if (isOnline)
    {
        [httpClient postRequest:@"/api/addAlbum" body:[album description]];
    }
}

- (void)deleteAlbumAtIndex:(int)index
{
    [persistencyManager deleteAlbumAtIndex:index];
    if (isOnline)
    {
        [httpClient postRequest:@"/api/deleteAlbum" body:[@(index) description]];
    }
}

```
看一下addAlbum:atIndex:.这个类第一次本地的更新数据，如果有网络连接，通过远程服务进行更新。这就是外观的真正力量，当你系统外的某个类添加一个新的album时，它不知道——当然也不需要知道——下层的复杂性。

>注意：当在你的子系统需要设计一个外观时，没有什么可以组织客户端直接访问这些"隐藏"类，不要吝啬防御代码，不要想当然的以为所有客户端一定会用与使用外观的方式一样来使用你的类。

编译并运行你的应用，你将会看到下面一些样的激动人心的空的黑屏幕。

![2.png](http://upload-images.jianshu.io/upload_images/2353580-0603ab4546daca68.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



你需要一些东西来让屏幕展示出数据——使用下一个设计模式对你来说很不错：装饰器。

# 装饰器设计模式

装饰器模式：在不改变对象代码的情况下，为对象动态的添加行为和职责。

在Objective-C中有两个非常常见的这个模式的实现：类别和代理。

## 类别

类别是一个十分强大的机制， 它允许你不需要子类化就可以为已存在的类添加方法。这个新的方法在编译时被添加，可以像其他方法一样被执行。它和装饰器的定义有稍许的不同，类别不能持有扩展类的实例。

>注意：不但可以扩展你自己的类，而且你可以给任何Cocoa类添加方法。

### 如何使用类别

想象一下这种情况，你有一个album对象，想要把它展示在一个tableview里面：

![design3.png](http://upload-images.jianshu.io/upload_images/2353580-800096f0722035b4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


album的标题从哪里来？Album是一个模型对象，它不关系你怎么展示这些数据。你需要一些额外的代码，添加方法到Album类，但是不能直接修改类的内容。


你将创建一个扩展子Album的类别，它定义了一个新方法，这个方法返回一个可以很容易被tabieview使用的数据结构。

这个数据结构看起来像下面的样子：

![delegate.png](http://upload-images.jianshu.io/upload_images/2353580-c65bbf3204135f99.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


添加Album的一个类别，使用 **File\New\File...** 选择 **Objective-C category** 模板——不要选择Objective-C class！在Category中输入 TableRepresentation并且在Category on 中输入Album。

>注意：你注意到了新文件的名字了吗？Album+TableRepresentation表示你扩展了Album类。这个约定是重要的，因为它是容易阅读的并且阻止了与你或者其他人可能创建其他的类别产生冲出。

进入Album+TableRepresentation.h文件，添加下面的方法声明：

```
- (NSDictionary*)tr_tableRepresentation;
```

看到在方法名的前面有tr_前缀，作为类别名字的缩写：TableRepresentation。同样的，像这样的约定可以阻止与其他的方法产生冲出。

>注意：如果类别中方法的名字与原始类中方法的名字一样，或者这这个类的另一个类别中有一样名字的方法(或者甚至是一个父类)，在运行时哪一个方法被调用时不明确的。如果你对自己的类使用类别，这种问题是微乎其微的，但是当你对标准的Cocoa 或者Cocoa Touch类使用类别添加方法是就会出现一系列的问题。

进入Album+TableRepresentation.m添加下面的方法：

```
- (NSDictionary*)tr_tableRepresentation
{
    return @{@"titles":@[@"Artist", @"Album", @"Genre", @"Year"],
             @"values":@[self.artist, self.title, self.genre, self.year]};
}
```
仔细想想这个模式的强大之处是什么：

1. 你可以从Album直接使用功能。
2. 你给Album类添加了东西但是没有子类化它，如果你需要创建Album的子类，你仍然可以那样做。
3. 你没有修改Album的任何代码，就让你得到了一个Album可以展示在tableview中的数据格式。

苹果公司在基础类中大量的使用了类别，看看他们是怎么做的，打开NSString.h。发现@interface NSString，你将会看到这个类定义了三个类别：NSStringExtensionMethods, NSExtendedStringPropertyListParsing and NSStringDeprecated。类别帮助你让方法有组织并且分成了许多部分。


### 代理

另一个装饰器设计模式，代理，是这样一种机制：一个对象的行为代表或者协调另一个对象。例如，当你使用TableView，你必须实现方法：tableView:numberOfRowsInSection:。

你不可能期待着TableView知道每一节会有多少行，因为这是程序特有的。因此，计算每一节有多少行的任务就交给了TableView 的代理。这允许TableView的展示不依赖于数据。

下面是一个模拟的过程，解释了当你新建一个TableView时都放生了什么：

![delegate2.png](http://upload-images.jianshu.io/upload_images/2353580-7d9d58ddeb8fece0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


TableView对象做它的工作去展示一个列表。然而，它终究需要一些它没有的信息，此时，它向它的代理发送消息询问额外的信息。在Objective-C的代理模式的实现中，一个类可以通过协议声明可选和必须的方法，稍后你将会了解协议是什么。

子类化一个对象然后重写必要的方法可能看起来更容易些，但是考虑到你只能子类化一个单一的类，如果你想一个对象是两个或者更多对象的代理，通过子类化是不可能实现的。

>注意：这是一个重要的模式，苹果公司在很多的UIKit类中使用它：UITableView, UITextView, UITextField, UIWebView, UIAlert, UIActionSheet, UICollectionView, UIPickerView, UIGestureRecognizer, UIScrollView。还远远不止这些。

### 如何使用代理模式

打开ViewController.m文件，在文件顶部添加下面的两条import语句：

```
#import "LibraryAPI.h"
#import "Album+TableRepresentation.h"
```
现在，添加这些私有变量到这个类的扩展中，类扩展看起来像下面的样子：

```
@interface ViewController () {
    UITableView *dataTable;
    NSArray *allAlbums;
    NSDictionary *currentAlbumData;
    int currentAlbumIndex;
}

@end
```
然后，在类的扩展中用下面这行替换掉@interface这一行：

```
@interface ViewController () <UITableViewDataSource, UITableViewDelegate> {
```

这是使你的代理遵守协议——把它想成是一个履行方法的合同的代理的承诺。这里，你指出了ViewController将要遵守UITableViewDataSource和UITableViewDelegate 协议。TableView要绝对的保证确保必须的方法被它的代理实现。

下一步，用下面的方法替换viewDidLoad: 

```
- (void)viewDidLoad
{
    [super viewDidLoad];
    // 1
    self.view.backgroundColor = [UIColor colorWithRed:0.76f green:0.81f blue:0.87f alpha:1];
    currentAlbumIndex = 0;
    
    //2
    allAlbums = [[LibraryAPI sharedInstance] getAlbums];
    
    // 3
    // the uitableview that presents the album data
    dataTable = [[UITableView alloc] initWithFrame:CGRectMake(0, 120, self.view.frame.size.width, self.view.frame.size.height-120) style:UITableViewStyleGrouped];
    dataTable.delegate = self;
    dataTable.dataSource = self;
    dataTable.backgroundView = nil;
    [self.view addSubview:dataTable];
}
```
对上面的代码进行分解：

1. 改变背景颜色为好看的深蓝色。
2. 通过API得到一组albums，你没有直接使用PersistencyManager。
3. 创建TableView，指明ViewController是TableView的代理和数据源。所以，ViewController将提供所有TableView需要的信息。

现在，添加下面的方法到ViewCont.m中：

```
- (void)showDataForAlbumAtIndex:(int)albumIndex
{
    // defensive code: make sure the requested index is lower than the amount of albums
    if (albumIndex < allAlbums.count)
    {
    	// fetch the album
        Album *album = allAlbums[albumIndex];
        // save the albums data to present it later in the tableview
        currentAlbumData = [album tr_tableRepresentation];
    }
    else
    {
        currentAlbumData = nil;
    }

    // we have the data we need, let's refresh our tableview    
    [dataTable reloadData];
}
```

showDataForAlbumAtIndex: 方法从数组中获取需要的数据，当你想要展示新的数据，只需要调用reloadData方法。使TableView请求代理下面这些事情：这个列表有多少个节，每个节有多少行以及每行应该长什么样子。

在viewDidLoad的最后添加下面的代码：

```
[self showDataForAlbumAtIndex:currentAlbumIndex];
```

在app开始时加载通用数据，由于currentAlbumIndex 被初始化为0，将展示集合中的第一个album。

编译并运行你的项目，程序将会崩溃，在调试控制台出现下面的异常信息。

![3.png](http://upload-images.jianshu.io/upload_images/2353580-dabd55c1727b020b.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


这是怎么了？你声明了ViewController为TableView的代理和数据源，但是，这样做了你必须遵守所有必须的方法——包括 tableView:numberOfRowsInSection:——你还没有实现。

在@implementation和@end之间的任何地方添加下面的代码：

```
- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section
{
    return [currentAlbumData[@"titles"] count];
}

- (UITableViewCell*)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"cell"];
    if (!cell)
    {
        cell = [[UITableViewCell alloc] initWithStyle:UITableViewCellStyleValue1 reuseIdentifier:@"cell"];
    }
    
    cell.textLabel.text = currentAlbumData[@"titles"][indexPath.row];
    cell.detailTextLabel.text = currentAlbumData[@"values"][indexPath.row];
    
    return cell;
}
```

tableView:numberOfRowsInSection:返回在列表中要展示的行数，这个数字是在数据结构中的标题数。

tableView:cellForRowAtIndexPath: 用标题和它的值创建并返回一个cell。

编译并运行你的项目，你的app应该正常运行并且像下面的样子：

![d1.png](http://upload-images.jianshu.io/upload_images/2353580-6b96494d42df8492.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)














