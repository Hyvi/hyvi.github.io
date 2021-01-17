---
title: "Customize Icon for Plantuml"
date: 2020-11-14T23:26:01+08:00
draft: false
tags: 
categories: 
featured_image: 
description: 
---

# 说明
记录如何定制 PlantUML 中的图标


# 操作 
*在mac下操作*

- 处理图片
- 编码生成 Sprite 
- 定义宏函数

## 处理图片
如果是png图片，则进行大小的裁剪，一般是48 * 48 px，如果非 png 图片，下面命令也会重新生成 48 像素的正方形图片。
```
qlmanage -t -s 48 -o . logo.svg 
```
*qlmanage 命令为 MAC 系统自带的*
## 对 PNG 的图片编码

```
java -jar ~/Downloads/plantuml.jar -encodesprite 16z logo.svg.png
```

生成的代码如下;

```
sprite $logo [48x48/16z] {
pPLNWWCX34F7zTt_n5imtbHcbhyedGYGXR6FJuRw6-YIdhn5hkdXBuZL12VbtRWa_cuO5aeLv9sQE1O8ycAHwwrRv2gqyv6hrGJiZ6yWfn6Tko6BO1UCbPSh
1GR79S1Ulvw7_E2bTVQwktHo3s94Q7jwEpqA9b1_L2Oh0txBW21gbjiF1Y5gV-9tE5LpK9EuEQMrI_5oxkVJ5WLhfXEJfYBZDr3JiBAYZpz-PMMjwr34W40E
SD0Pc_P7JlwWPMOCbOuPQT0nUclErdCxOd354tLeqtDyb9uPB-tkj3H7g9MNmhqpGPQT-eEIIht5O4hPMHBwl9H2hHZatD4eo3olpWUD0JyiueSLUaXbWNg4
PHdZ_yqt2QdGz_9vyxxitiVD-xvVJ_RhrNuztA-t-_Lylr_izwFzVhVkfxBPhpyPtm
}

```

## 定义宏函数
定义宏函数，加入资源文件里，通过 !inlcude 的方式引入资源文件。这里是为了其他地方更方便的引用。

```
!define EMQX(_alias, e_label) rectangle "<color:black><$emqx></color>\r e_label" as _alias <<EMQX>>
```

# 最后
...记录下来而已

<br>

<center>  ·End·  </center>
