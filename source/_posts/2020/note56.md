---
title: HTTP学习笔记（三）
tags:
  - http
categories:
  - http
date: 2018-08-13 19:56:48
---

## HTTP报文信息
HTTP报文本身由多行数据构成的字符串文本。大致分为报文首部和报文主体两块，由（CR+LF）来划分。通常并不一定要有报文主体。
<!-- more -->
### 请求行
包含用于请求的方法，请求的URI和HTTP版本。
### 状态行
包含表明响应结果的状态码，原因短语和HTTP版本。
### 首部字段
包含表示请求和响应的各种条件和属性的各类首部。
通用首部，请求首部，响应首部，实体首部。
### 其他
如cookie等。

## 压缩传输的内容编码
常用的内容编码有：
gzip，compress，deflate，identity。

## 分割发动的分块传输编码

分块传输编码将实体主体分成多个部分，有客户端负责解码，恢复到编码前的实体主体。

## 发动多种数据的多部分对象集合

对部分对象集合包含的对象如下：

### multipart/form-data
在web表单文件上传时使用。
### multipart/byteranges
状态码206，响应报文包含了多个范围的内容时使用。获取部分内容的范围请求。