---
title: unwindSegue 实现界面跳转
date: 2017-06-30 13:36:53
categories:
- iOS
tags:
- iOS
- 界面跳转
- unwindSegue
---

传统的界面跳转方法：

```swift
//ThirdViewController
@IBAction func pop(_ sender: Any) {
	navigationController?.popViewController(animated: true)
}
	
@IBAction func popToRoot(_ sender: Any) {
	navigationController?.popToRootViewController(animated: true)
}
//ForthViewController
@IBAction func dismiss(_ sender: Any) {
	dismiss(animated: true, completion: nil)
}



```
<!-- more -->

使用unwindSegue实现界面跳转：

```swift
//RedViewController
@IBAction func unwindToRed(sender: UIStoryboardSegue){
	if sender.identifier == "FromGreenToRed" {
		print("from green")
	} else if sender.identifier == "FromYellowToRed" {
		print("from yellow")
	}
}
//GreenViewController
@IBAction func unwindToGreen(sender: UIStoryboardSegue){
    
}
//YellowViewController
@IBAction func unwindToYellow(sender: UIStoryboardSegue){
    
}
```