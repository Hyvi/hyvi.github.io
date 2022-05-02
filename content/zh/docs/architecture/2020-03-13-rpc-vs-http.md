---
title: "RPC vs Http"
date: 2020-03-15T00:00:32+08:00
draft: false
tags:
categories:
featured_image:
description:
---

在评估 4G SDK 方案中，嵌入同事方案中使用 RPC 方案与服务器通信，让我感觉很奇怪，因为在我们的 web server 里通信一般都是 https 通信方式。

## RPC
wikipedia's List of network protocols (OSI model)

RPC 属于 Session Layer,

## HTTP vs RPC

![](https://pic1.zhimg.com/80/v2-7d859132076fe279e570ffcd6e7545d8_720w.jpg)

rpc 是远端过程调用，其调用协议通常包含传输协议和序列化协议。

传输协议包含：如著名的 [gRPC](grpc / grpc.io) 使用的 http2 协议，也有如 dubbo 一类的自定义报文的 tcp 协议。
序列化协议包含：如基于文本编码的 xml json，也有二进制编码的 protobuf hessian 等。


## HTTP 长连接
在参考<sup>[2]</sup> 中提到 httpServer 怎么处理长连接的： httpServer 创建一个 goroutine，更确切的说，是为了为一个新的 tcp 连接去创建一个 goroutine， 详细参考文章的源码。

## Compare gRPC services with HTTP APIs
gRPC is designed for HTTP/2, vs HTTP 1.x:

- binary framing and compression.
- Multiplexing of multiple HTTP/2 calls over a single TCP connection. Multiplexing eliminates [head-of-line-blocking](#head-of-line-blocking)

| Feature          | gRPC                                               | HTTP APIs with JSON           |
| ---------------- | -------------------------------------------------- | ----------------------------- |
| Contract         | Required (`.proto`)                                | Optional (OpenAPI)            |
| Protocol         | HTTP/2                                             | HTTP                          |
| Payload          | [Protobuf (small, binary)](#performance)           | JSON (large, human readable)  |
| Prescriptiveness | [Strict specification](#strict-specification)      | Loose. Any HTTP is valid.     |
| Streaming        | [Client, server, bi-directional](#streaming)       | Client, server                |
| Browser support  | [No (requires grpc-web)](#limited-browser-support) | Yes                           |
| Security         | Transport (TLS)                                    | Transport (TLS)               |
| Client code-generation | [Yes](#code-generation)                      | OpenAPI + third-party tooling |

> 表格来自 https://docs.microsoft.com/en-us/aspnet/core/grpc/comparison

### Head-of-line Blocking

> 详细描述了HOL https://engineering.cred.club/head-of-line-hol-blocking-in-http-1-and-http-2-50b24e9e3372

Key Points: 

- Frame
- Message 
- Stream

The HOL Blocking issue is resolved at the HTTP layer in HTTP/2, but it now moves to the TCP layer.

HTTP/3 or QUIC solves HOL Blocking at TCP layer by leveraging UDP instead of TCP as the transport protocol.

## 参考

1. 既然有 http，为什么还要 RPC 调用？
  https://www.zhihu.com/question/41609070

2. Golang httpServer 对 KeepAlive 长连接的处理方式
  https://blog.csdn.net/jeffrey11223/article/details/81222774

<br>

<center>  ·End·  </center>
