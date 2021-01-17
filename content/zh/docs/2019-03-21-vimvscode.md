---
layout: post
title: "VIM转VSCODE"
description: ""
categories: 
tags: 
- vim
---

VIM适合折腾  
VS Code 适合高效率业务开发  
开始学习VS Code的快捷键   

<br />
还在用VIM...有毒?   
Update At 2019.07.08


vim-go为什么错误这么让人不知所措，比如：   
```bash 
gorename: can't find package containing
```
```bash 
gometalinter: unkown linters: govet, typecheck, unsed, gosimple
```
```bash 
--enable-all/--disable-all can not be combined 
```
``` bash 
quickfix 没有显示出来, 并且仅仅提示 GoMetaLinter Failed
```
解决办法有很多种，而在不断尝试过程中解决问题：  

+ 对vim-go配置详细了解, 比如`g:go_metalinter_enabled`和`g:go_metalinter_autosave_enabled`
+ 更换最新的版本, 比如vim-go和golangci-lint的最新稳定版本, 比如gorename最新版本并不支持go modules项目

不深入了解vim-go的原理，用不来vim-go， 期望：某天能跟vscode golang插件一样好用   
不过，在使用vim-go的过程中，对静态代码检查工具有了更多了解，比如有对golang代码的安全检查: gosec    
Updated At Thu Jul 18 13:34:37 2019
