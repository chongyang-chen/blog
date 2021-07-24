---
title: HTTP学习笔记（二）
tags:
  - http
categories:
  - http
date: 2018-08-13 19:56:45
---

## HTTP协议
HTTP协议用于客户端和服务器之间的通信。
<!-- more -->

### 通过请求与响应的交换达成通信

请求报文由请求方法，请求URI，协议版本，可选的请求首部字段和内容实体构成。

```
GET /index.html HTTP/1.1
Host: ccyag.com
```
服务器响应结果：

```
HTTP/1.1 200 OK
Date: 2018-08-13 20:41:40
Content-Length: 354
Content-Type: text/html

<html>
......
```
响应报文基本由协议版本，状态码，原因短语，可选的响应首部字段和实体主体构成。

## HTTP是不保存状态的协议

虽然HTTP是无状态协议，但为了实现期望的保持状态功能，引入了cookie技术。

## HTTP方法

GET，POST等。

## 持久连接节省通信量

在TTTP/1.1中，所有的连接默认都是持久连接。

### 管线化（pipelining）

同时并行发送多个请求。

## 使用cookie管理状态
