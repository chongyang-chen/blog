---
title: 把时间戳转换成指定格式的字符串
date: 2017-06-30 14:14:20
categories:
- iOS
tags:
- iOS
- 时间戳
---
>时间戳是指格林威治时间1970年01月01日00时00分00秒(北京时间1970年01月01日08时00分00秒)起至现在的总秒数。 

把时间戳转换成指定格式的字符串，有时候服务器会返回给你类似 1498803231 的一长串数字，需要把它转换成人们可以理解的时间格式。具体实现方法如下：

<!-- more -->

```swift

func timeStampToString(_ timeStamp:Int)->String {
	//如果是毫秒的话，需要执行下面一句
	let timeSta = timeStamp / 1000
	let dfmatter = DateFormatter()
	//制定日期显示格式
	dfmatter.dateFormat="YYYY-MM-dd HH:mm:ss"
	let date = Date(timeIntervalSince1970: TimeInterval(timeSta))
	return dfmatter.string(from: date)
}

```
