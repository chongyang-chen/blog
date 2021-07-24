---
title: CSS 基础知识
tags:
  - css
categories:
  - css
date: 2016-09-30 13:59:24
---

上文总结了HTML的基础知识，今天来学习一下CSS的基础知识。 ***《HTML5与CSS3基础教程(第8版)》*** 基础知识总结。

<!-- more -->

### CSS 构造块

#### 语法规则：

```css
h1 {
    color: red;
}
```

#### 注释

`/*  ... */`

#### 理解继承与冲突

继承可以简化样式表，对于多数属性，可以使用 **inherit** 强制进行继承。

当发生冲突时，应考虑特殊性，顺序，和重要性来判断哪个规格应该起作用。

#### 属性值

每个 CSS 属性可以接受那些值都有不同的规定，有的接受预定义的值，有的接受数字，整数，百分数，URL，颜色，相对值。

### 样式表

#### 创建外部样式表

将代码写入CSS文件，文件的扩展名为 css。

#### 创建嵌入式样式表

style 元素包围的样式规则，通常位于 head 部分。

#### 内联样式表

内联样式是在 HTML 中应用 CSS 的第三种方式。不过，应当最后考虑这种方式，因为它将内容(HTML)和表现(CSS)混在了一起，严重地违背了最佳实践。

#### 媒体相关的样式表

可以指定一个只用于特定输出的样式表， 如只用于打印，或只用于在浏览器中查看屏幕。例如，可以创建一个具有打印和屏幕版 本共有特征的通用样式表，再创建单独的打印样式表和屏幕样式表，分别包含只用于打印的属性和只用于屏幕显示的属性。

### 选择器

#### 名称选择器

```css
p {
    color: red;
}
```

#### 类或ID选择器

```css
.architect {
    color: red;
}
```

#### 上下文选择元素

```css
.architect p {
    color: red;
}

```

architect 类元素后代的 p 元素。

```css
.architect > p {
    color: red;
}

```

architect 类元素的子元素 p 元素。

```css
.architect p+p {
    color: red;
}

```
相邻同胞结合符只选择直接跟在同胞 p 元素之后的元素。

#### 选择第一个或者最后一个元素

**:first-child** 或者  **:last-child**

#### 选择元素的第一个字母或第一行

**:first-letter** 或者 **:first-line**

#### 链接元素

```css
/* 未访问的链接，为红色 */
a:link {
	color: red;
}

/* 访问过的链接，为橙色 */
a:visited {
	color: orange;
}

/* 获得焦点的链接，为紫色 */
a:focus {
	color: purple;
}

/* 鼠标停留的链接，为绿色 */
a:hover {
	color: green;
}

/* 激活的链接，为篮色 */
a:active {
	color: blue;
}

```
顺序可以为 LVFHA 或者 LVHFA 。

#### 按属性选择元素

```css
p[class] {
	color: red;
}

```
所有具有class属性的段落。

#### 元素组

```css
h1, h2 {
	color: red;
}
```

