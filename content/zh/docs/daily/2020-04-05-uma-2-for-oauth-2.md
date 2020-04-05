---
title: "User-Managed Access (UMA) 2.0 Grant for OAuth 2.9 Authorization"
date: 2020-04-05T17:32:13+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

# 背景
在阅读<OAuth2.0实战>中提到UMA协议，在书中只是简单的提到这个协议，没有详细的讲解这个协议，有点懵，所以在此整理相关的资料，对其深入了解。 

## UMA的重要性
为什么了解UMA？UMA能管理用户对用户的共享，还能管理由用户控制的授权服务器。具体的场景：如果想使用第三方服务打印照片的人不是ALice自己，而是Alice的好友Bob，他想打印Alice的账户中属于他们俩的音乐会照片，该如何实现？

- Alice可以让照片打印服务使用她自己的个人授权服务器。她可以在授权服务器设置这样的策略：“当Bob到来时，让他读取所有的照片。”
- 然后Alice的授权服务器会要求Bob用一组**声明**证明自己的身份。只要Bob提供的信息和ALice设置的策略相匹配，则Bob的打印服务就可以访问Alice共享给他的照片，而不需要冒充Alice的身份。Bob也不需要登录到Alice的鉴权服务器。

## UMA的工作原理
UMA成为一个相当复杂的多步骤协议，并且具有许多参与方和活动部件，它正因此成为一个功能强大的协议，能够解决其他技术无法解决的问题。
![UMA Flow from OAuth 2 实战](https://hyvi.github.io/blog-images/20200405/uma-flow.png)

考虑点：资源拥有者的凭据和请求方的凭据都没有被透露给资源服务器或客户端。另外，这两方也没有相互透露敏感的跟人信息。请求方只是最小限度的提供证明信息，满足资源拥有者设置的策略即可。 

# 实践

- Pauldron, an experimental authorization server based on OAuth 2.0 and User-Managed Access (UMA) profile of OAuth 2.0 with additional extensions 貌似是1.0版本的UMA协议.
# 参考
1. User-Managed Access(UMA) 2.0 Grant for OAuth 2.0 Authorization 
  https://docs.kantarainitiative.org/uma/wg/rec-oauth-uma-grant-2.0.html

2. UMA 2.0 的实现
  https://kantarainitiative.org/confluence/display/uma/UMA+Implementations

3. UMA Home 官网吧
  https://kantarainitiative.org/confluence/display/uma/Home

<br>

<center>  ·End·  </center>
