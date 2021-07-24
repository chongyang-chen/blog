---
title: iOS Swift Games 学习笔记（1）
categories:
  - swift
tags:
  - games
  - swift
date: 2021-03-15 10:28:08
---

今天学习iOS 游戏开发。Xcode 12.4，Swift 5，mac OS Big Sur 11.2.3。

<!-- more -->

使用Xcode新建一个游戏项目：

选择iOS平台，Game，点击Next。

<img src="01.png" width=680px>

选择Swift，SpriteKit，点击Next。

<img src="02.png" width=680px>

运行程序：

<img src="03.png" width=480px>

修改代码：

```swift
class GameScene: SKScene{
    
    let backgroundNode = SKSpriteNode(imageNamed: "Background")
    let playerNode = SKSpriteNode(imageNamed: "Player")
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
    }
    
    override init(size: CGSize) {
        super.init(size: size)
        backgroundNode.size.width = frame.size.width;
        backgroundNode.anchorPoint = CGPoint(x: 0.5, y: 0.0)
        backgroundNode.position = CGPoint(x: size.width / 2.0, y: 0.0)
        addChild(backgroundNode)
        playerNode.position = CGPoint(x: size.width / 2.0, y: 80.0)
        addChild(playerNode)
    }
}
```



运行程序：

<img src="04.png" width=480px>