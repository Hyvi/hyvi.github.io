---
title: "RPC vs Http"
date: 2020-03-15T00:00:32+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

在评估4G SDK方案中，嵌入同事方案中使用RPC方案与服务器通信，让我感觉很奇怪，因为在我们的web server里通信一般都是https通信方式。  


# HTTP vs RPC

![](https://pic1.zhimg.com/80/v2-7d859132076fe279e570ffcd6e7545d8_720w.jpg)  

rpc是远端过程调用，其调用协议通常包含传输协议和序列化协议。  

传输协议包含: 如著名的 [gRPC](grpc / grpc.io) 使用的 http2 协议，也有如dubbo一类的自定义报文的tcp协议。  
序列化协议包含: 如基于文本编码的 xml json，也有二进制编码的 protobuf hessian等。  


# 参考

1. 既然有http，为什么还要RPC调用？  
  https://www.zhihu.com/question/41609070  


<br>

<center>  ·End·  </center>
