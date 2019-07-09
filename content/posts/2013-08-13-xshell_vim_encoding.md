---
layout: post
title: "fencview.vim + xshell + vim + 各种中文编码问题"
description: "fencview.vim "
categories: 
- Tech
tags: [vim, xshell]
---
 

c++ 老代码都不是utf-8编码，估计是gb2312或gbk编码，而javascript是utf-8编码  
咋办？   
vim中只设置过  
  "set encoding=gb2312 termencoding=utf-8 "fileencoding=gbk   

不同编码文件，怎么通过一个设置来搞定呢？ 疑惑！！！  
以前碰到不同文件后缀名能用不同的高亮，不同的格式化。    
按此逻辑。。。  
不同的文件编码可以用不同的配置咯。  

google 就如上帝！！！  

发现了 http://edyfox.codecarver.org/html/vim_fileencodings_detection.html   
最后提到了统一解决办法 fencview.vim   

杜绝眼高手低：搞起

一个小时...  
两个小时...  
搞定   
1. 下载插件：fencview  
2. 配置.vimrc 
``` bash 
set encoding=utf-8
set termencoding=utf-8 "fileencoding=utf-8
set fileencodings=utf-8,ucs-bom,gb18030,gbk,gb2312,cp936
let g:fencview_autodetect=1
"let g:fencview_auto_patterns='*'
```
最后一行注释掉： 因为不注释javascript 文件不高亮。
