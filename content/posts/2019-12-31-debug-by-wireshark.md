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

### 为什么不能代理所有的HTTP请求
因为在操作系统层面，没有“HTTP request”这一概念，只有TCP连接。  
Contacting a HTTP proxy means changing the HTTP request slightly as well as contacting the proxy server instead of the host named in the URL.  
所以这个逻辑是写在发送HTTP requests的软件代码里。  
curl和wget有他们自己的实现HTTP Request的代码，并使用了自己的配置文件（-x选项）。两者都没有实现基于配置的逻辑，也没有使用Mac OS 系统提供的HTTP Libraries(这个库使用了代理设置）  

## charles
原理类似fiddler，但是mac上使用的简单的工具.

## mitmproxy
原理是中间人的方式来实现, 再加个proxy, 中间人代理软件，可以用来拦截、修改、保存HTTP/HTTPS请求。  
> An interactive console program than allows traffic flows to be intercepted, inspected, modified and replayed. 
优点是可自定制化开发，命令行模式，适合code geek和键盘控

###  安装和使用 
[MitmProxy 使用教程 for MAC](http://rui0.cn/archives/498)  
更关心[Transparent Proxying使用](https://docs.mitmproxy.org/stable/howto-transparent/#macos)  

### Transparent Proxying 在Mac上实践 
参考官方文档，对mac下进行全局抓包的尝试。  

## wireshark
抓取网卡上的所有TCP、UDP的数据  

### HTTPS的解密

![TLS SSL for wireshark](https://support.citrix.com/files/public/support/article/CTX116557/images/0EM0z000000BGxv.jpeg)  

- 通过私钥来解密, 咨询过运维，这种私钥是没办法提供的。  参考这边文档： [How to Decrypt SSL and TLS Traffic Using Wireshark](https://support.citrix.com/article/CTX116557)  
- `适合浏览器`通过设置环境变量截取浏览器的pre_master_secret,进而实现解密HTTPS的目的。 [wireshark两种解密https方式](https://www.cnblogs.com/yurang/p/11505741.html)   
- `也只适合浏览器，其他客户端发送出的请求无法解密?` 通过mitmproxy来获取SSLKEYLOGFILE， 参考 [Wireshark and SSL/TLS Master Secrets](https://docs.mitmproxy.org/stable/howto-wireshark-tls/) `#TODO`

 This mechanism (SSLKEYLOGFILE) currently(2019) does not work for Safari, Microsoft Edge, and others since their TLS libraries (Microsoft SChannel / Apple SecureTransport) do not suppport this mechanism.   
This mechanism works for applications other than web browser as will but it dependent on the TLS Libraries used by application. Examples of applications: 

- Applicaitons using OPENSSL conld use `GDB or a LB_PRELOAD trick` to extract the secrets . 
- For Java programs  
- Python scripts can be edited to dump keys as well 


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
[怎么让charles能代理所有的http(s)的请求呢？](https://superuser.com/questions/398977/how-can-i-run-all-http-requests-through-charles-web-debugging-proxy-including)  

<br>

<center>  ·End·  </center>
