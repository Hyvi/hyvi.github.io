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

# 名词解释
**HTTP Strict transport security(HSTS)**  
HTTP严格传输安全   
HSTS禁止浏览器使用无效证书。  
  

**Certificate Transparency**  
为了解决CA存在的问题（故意或者恶意签发证书等），目的是提供一种开发的审计和监控系统，可以让任何域名所有者或者CA确定证书是否被错误签发或者被恶意使用，从而提供HTTPS网站的安全性。  
[ how ct works ](https://www.certificate-transparency.org/how-ct-works)   

**HTTP Public Key Pinning**  
用来防范由「伪造或不正当的手段获得网站证书」造成中间人攻击。  
工作原理： 通过响应头或者<meta>标签告诉浏览器当前网站的证书指纹，以及过期时间等其他信息.  
Google已经针对不验证服务器证书的APP给出了警告，这些APP将来会有被Play store拒之门外的危险,[参考](https://support.google.com/faqs/answer/6346016?hl=en)   

> Chrome 69 版本开始移除对HPKP的支持  

**OCSP Stapling**  
OCSP(Online Certifacte Status Protocol, 在线证书状态协议)是用来检验证书合法性的在线查询服务。   
TLS握手阶段，实时查询OCSP接口，并在获得结果前阻塞后续流程。但导致建立TLS连接时间变得更长。 而 OCSP Stapling, 是服务器主动获取OCSP查询结果并随着证书一起发给客户端，从而让客服端跳过自己去验证的过程，提高TLS握手效率  

# 工具
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

- Regurlar
- Transparent
- Reverse Proxy
- Upstream Proxy
- SOCKS Proxy


![ Modes of Operation](https://docs.mitmproxy.org/stable/schematics/proxy-modes-flowchart.png)   
### 透明代理
重定向机制，可以将目的地为Internet上的服务器的TCP连接透明地重新路由到侦听代理服务器上。这通常采用与代理服务器相同的主机上的防火墙形式。比如Linux下的iptables\或者OSX中的pf。具体如何操作见参考中的"Mac 上使用mitmproxy对ios app进行抓包”   


###  安装和使用 
[MitmProxy 使用教程 for MAC](http://rui0.cn/archives/498)  
更关心[Transparent Proxying使用](https://docs.mitmproxy.org/stable/howto-transparent/#macos)  

#### Transparent Proxying 在Mac上实践 
参考官方文档，对mac下进行全局抓包的尝试。如下：   

- Enable IP forwarding.

```bash 
sudo sysctl -w net.inet.ip.forwarding=1
```

- Place the following two lines in **/etc/pf.conf**.

```bash
rdr pass on en0 inet proto tcp to any port {80, 443} -> 127.0.0.1 port 8080
```
This rule tells pf to redirect all traffic destined for port 80 or 443 to the local mitmproxy instance running on port 8080. You should replace `en0` with the interface on which your test device will appear.

> rdr rules in pf.conf above apply only to inbound traffic. They will NOT redirect traffic coming from the box running pf itself.

- Configure pf with the rules.

```bash
sudo pfctl -f pf.conf
```
Mac系统默认使用/etc/pf.conf， 调式完之后需要重置 
- And now enable it.

```bash
sudo pfctl -e
```

- Fire up mitmproxy.

You probably want a command like this:
```bash
mitmproxy --mode transparent  --showhost
```

The `--mode transparent` option turns on transparent mode, and the `--showhost` argument tells
mitmproxy to use the value of the Host header for URL display.

- Finally, configure your test device.

Set the test device up to use the host on which mitmproxy is running as the default gateway and install the mitmproxy certificate authority on the test device   
   
到此, 可以抓包en0显卡上的流量, 但是抓包不了Mac本地上的流量。   
但是这并没有解决抓包APP里HTTPS的流量问题，因为出现如下错误：  
“ warn: 192.168.2.3:56243: Client Handshake failed. The client may not trust the proxy's certificate for e.crashlytics.com.  "   
解决办法见： "破解SSL Pinning" 


另外上述方法也没有办法抓包本机电脑上的流量； 需要进一步设置： [Work-around to redirect traffic originating from the machine itself](https://docs.mitmproxy.org/stable/howto-transparent/)   
-  pf解决Mac自身流量抓包

```bash 
#The ports to redirect to proxy
redir_ports = "{http, https}"

#The address the transparent proxy is listening on
tproxy = "127.0.0.1 port 8080"
#The user the transparent proxy is running as
tproxy_user = "nobody"

#The users whose connection must be redirected.
#
#This cannot involve the user which runs the
#transparent proxy as that would cause an infinite loop.
#

rdr pass proto tcp from any to any port $redir_ports -> $tproxy
pass out route-to (lo0 127.0.0.1) proto tcp from any to any port $redir_ports user { != $tproxy_user }
```
转发处理nobody之外的所有用户的流量到mitmproxy上。 为了避免循环，所以以nobody用户身份来启动mitmproxy。  
```bash
sudo -u nobody mitmproxy --mode transparent --showhost
```

** 发现有些流量不见了 ** 
排查发现因为wifi下启用了socks代理，导致一些流量不见了, 转发到shadowsocks socks5代理去了。  

#### 使用socks5的方式抓包所有的流量 
[Tracing All Network Machine Traffic Using MITMProxy for Mac OSX](https://blogs.msdn.microsoft.com/aaddevsup/2018/04/11/tracing-all-network-machine-traffic-using-mitmproxy-for-mac-osx/)  
跟regular proxy一样，需要client/应用支持或者更改。比如chrome更改网络方式为代理模式。比如不能对Curl的请求抓包不了  
同理，socks5也存在透明代理，不过实现的方式不一样, 比如tsocks

>  tsocks provides transparent network access through a SOCKS version 4 or 5 proxy (usually on a firewall). tsocks intercepts the calls applications make to establish TCP connections and transparently proxies them as necessary.

### 破解https的SSL Pinning TODO
[APP上破解https的SSL Pinning](https://crifan.github.io/app_capture_package_tool_charles/website/how_capture_app/complex_https/https_ssl_pinning/)  

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


# 参考
在Trello上记录所有待办事项。   
[常用的HTTP抓包工具Fiddler之使用技巧](https://zhuanlan.zhihu.com/p/47003094)     
[三种解密HTTPS流量的方法](https://imququ.com/post/how-to-decrypt-https.html)  
[杀手锏：如果让不支持代理的软件，通过代理进行联网](https://program-think.blogspot.com/2019/04/Proxy-Tricks.html#head-6)   
[如何使用透明代理抓HTTPS](https://www.javazhiyin.com/42166.html)  
[Mac 上使用mitmproxy对ios app进行抓包]( https://www.zoulei.net/2018/05/25/mitmproxy_transparent_model_network_capture/) 比较详细的操作  
[怎么让charles能代理所有的http(s)的请求呢？](https://superuser.com/questions/398977/how-can-i-run-all-http-requests-through-charles-web-debugging-proxy-including)  
[HTTP Public Key Pinning 介绍](https://imququ.com/post/http-public-key-pinning.html)  
[app 抓包利器.pdf](https://crifan.github.io/app_capture_package_tool_charles/website/)  

<br>

<center>  ·End·  </center>
