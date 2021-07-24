---
title: JavaScript基础（二）
date: 2017-06-21 09:40:05
categories:
- JavaScript
tags:
- JavaScript
---


JavaScript 能够直接写入 HTML 内容。

JavaScript 能改变 HTML 元素的内容。

JavaScript 能改变 HTML 元素的样式。

<!-- more -->

代码如下：



```html

<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8" />
		<script>
		//修改元素内容
		function changeContent()
		{
			x=document.getElementById("content");  // 找到元素
			x.innerHTML="Hello JavaScript!";    // 改变内容
		}
		//修改元素样式
		function changeStyle()
		{
			x=document.getElementById("style") // 找到元素
			x.style.color="#ffdddd";          // 改变样式
		}

		</script>
		<title>JavaScript 学习笔记</title>
	</head>
	<body>
		<p>
  			JavaScript 能够直接写入 HTML 内容：
		</p>
		<script>
			document.write("<h3>Hello world!</h3>");
			document.write("<p>世界你好！</p>");
		</script>
		<button type="button" onclick="alert('Ohhh!')">点它!</button>

		<p id="content">
			JavaScript 能改变 HTML 元素的内容。
		</p>
		<button type="button" onclick="changeContent()">修改上面的内容</button>
	
		<p id="style">
			JavaScript 能改变 HTML 元素的样式。
		</p>
		<button type="button" onclick="changeStyle()">修改上面的样式</button>
		
	</body>
</html>
```

