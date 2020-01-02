---
title: "抓包工具分析之完全攻略"
date: 2019-12-31T11:45:50+08:00
draft: false
tags: 
categories: 
- Tech

featured_image: 
description: 
---

# 背景
抓包分析是调式前后端协议的杀手锏，用好工具节省大量的时间去写代码优化代码。 

# 利器
有fiddler, charles, wiresharks,

## fiddler
使用中间人（man-in-middle）的方式来实现的。
- 本地化的工具，是一个使用本地127.0.0.1:8888 的HTTP代理。 
~任何能够设置HTTP代理为127.0.0.1:8888的浏览器和应用程序都可以使用Fiddler~
 
## charles
原理类似fiddler，但是mac上使用的简单的工具.

## wireshark
抓取网卡上的所有TCP、UDP的数据  

### HTTPS的解密

![TLS SSL for wireshark](https://support.citrix.com/files/public/support/article/CTX116557/images/0EM0z000000BGxv.jpeg)  

- 通过私钥来解密, 咨询过运维，这种私钥是没办法提供的。  参考这边文档： [How to Decrypt SSL and TLS Traffic Using Wireshark](https://support.citrix.com/article/CTX116557)  
- `适合浏览器`通过设置环境变量截取浏览器的pre_master_secret,进而实现解密HTTPS的目的。 [wireshark两种解密https方式](https://www.cnblogs.com/yurang/p/11505741.html)   

## mitmproxy 

### 透明代理
重定向机制，可以将目的地为Internet上的服务器的TCP连接透明地重新路由到侦听代理服务器上。这通常采用与代理服务器相同的主机上的防火墙形式。比如Linux下的iptables\或者OSX中的pf。具体如何操作见参考中的"Mac 上使用mitmproxy对ios app进行抓包”   

# 参考
在Trello上记录所有待办事项。   
[常用的HTTP抓包工具Fiddler之使用技巧](https://zhuanlan.zhihu.com/p/47003094)     
[三种解密HTTPS流量的方法](https://imququ.com/post/how-to-decrypt-https.html)  
[杀手锏：如果让不支持代理的软件，通过代理进行联网](https://program-think.blogspot.com/2019/04/Proxy-Tricks.html#head-6)   
[如何使用透明代理抓HTTPS](https://www.javazhiyin.com/42166.html)  
[Mac 上使用mitmproxy对ios app进行抓包]( https://www.zoulei.net/2018/05/25/mitmproxy_transparent_model_network_capture/) 比较详细的操作  
<br>

<center>  ·End·  </center>
