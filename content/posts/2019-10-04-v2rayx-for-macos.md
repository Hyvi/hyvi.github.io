---
title: "SS 全军覆没，v2ray for Macos"
date: 2019-10-04T16:14:08+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

# 简介
大国国庆，机会所有的ss挂了，查个个资料什么的确实不方便，一度使用了bing.com的“网页快照”来查看被墙的资料。  
国庆期间，陪完家人，开始搬砖。   
ss不能使用后，发现手机上v2ray 连上wifi时，是可以正常使用的（之前配置过服务器）.    
这次配置电脑上的v2ray client, 之前安装过v2rayx, 但是使用时出现无法连接的问题，加上UI版的配置无心使用, 这次把命令行的方式献上   

# 安装v2ray  
``` bash 
brew tap qiwihui/v2ray   
brew install v2ray-core  
```
没有被强  


# 配置v2ray
参考 [config.json](https://raw.githubusercontent.com/Dosimz/v2ray-config.json/master/config.json)   
修改inbound.port，outbound里的address和port，users中的id和security  
``` bash 
vim /usr/local/etc/v2ray.config.json 
```

# 启动v2ray + SwitchyOmega 
ss 也有用到SwtichyOmega，这次只需要启动v2ray   
```bash 
v2ray -config=/usr/local/etc/v2ray.config.json
```
开机启动的方式（亲测失败）   
``` bash 
brew services start v2ray-core 
```
<br>

<center>  ·End·  </center>
