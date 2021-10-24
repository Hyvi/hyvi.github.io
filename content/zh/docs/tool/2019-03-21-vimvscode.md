---
layout: post
title: "VIM 转 VSCODE"
description: ""
categories:
tags:
- vim
---

VIM 适合折腾
VS Code 适合高效率业务开发
开始学习 VS Code 的快捷键

<br />
## 更新记录
2019.07.08 还在用 VIM... 有毒？ 

2021-10-24 继续使用，发现各种好特性，比如在一行中删除光标后所有字符到有括号")"，这些技巧提升了效率。以防忘记，统一在这里记录，便于翻阅。


## 常用的编辑快捷键

### Editing 

To delete forward up to character 'X' type `dtX`

To delete forward through character 'X' type `dfX`

To delete backward up to character 'X' type `dTX`

To delete backward through character 'X' type `dFX`

### Navigation


## 历史
vim-go 为什么错误这么让人不知所措，比如：
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
quickfix 没有显示出来，并且仅仅提示 GoMetaLinter Failed
```
解决办法有很多种，而在不断尝试过程中解决问题：

+ 对 vim-go 配置详细了解，比如`g:go_metalinter_enabled`和`g:go_metalinter_autosave_enabled`
+ 更换最新的版本，比如 vim-go 和 golangci-lint 的最新稳定版本，比如 gorename 最新版本并不支持 go modules 项目

不深入了解 vim-go 的原理，用不来 vim-go， 期望：某天能跟 vscode golang 插件一样好用
不过，在使用 vim-go 的过程中，对静态代码检查工具有了更多了解，比如有对 golang 代码的安全检查：gosec
Updated At Thu Jul 18 13:34:37 2019
