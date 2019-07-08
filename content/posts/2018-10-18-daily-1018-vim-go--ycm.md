---
layout: post
title: "Daily 1018 vim go + Ycm"
description: ""
categories: 
tags: []
---
 


记录配置vim+go开发环境de折腾过程. 

## 输入"."点号后没有任何提示,不知所措，甚至怀疑就到这里了。 

当没有日志，我无从下手解决问题。  
我更新了所有的go库，重装了go-code/vim-go，依然没有解决，没有给我任何错误提示。  
开始怀疑“人生苦短，我用python"，  
不服输，爱折腾。  

我重装了vim-go/ gocode之后，我开始怀疑ycm这个玩意。   

原来真的是需要升级，而且安装时要注意go   

""" 
/.vim/bundle/YouCompleteMe$ ../install.sh --clang-completer --go-completer

""" 
安装时，加上go-completer的参数  


最后重启了 ycm服务器  
大功告成!!!

## 参考

[Autocomplete stopped working](https://github.com/fatih/vim-go/issues/659) 当我看完这个时，我确定了gocode没有问题。问题可能在ycm;   

[YouCompleteMe 支持 golang vim 自动补全](https://blog.csdn.net/haidonglin/article/details/78411968)   

[用VIM写GOLANG踩坑](http://qwding.github.io/post/vim_golang/) 这里提到为什么go自动提示的那么慢，原因就在go而非ycm, 最后autobuild的操作置为false  
