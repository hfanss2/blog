[English](https://gitee.com/iyohei/material-plus/blob/master/README.md)

## 主题介绍

本主题基于 [material-x](https://xaoxuu.com/wiki/material-x/) 主题魔改，原作者 [小吴博客](https://www.wushile.top/)（目前已失去维护） ，在征得作者同意下开源。此版本在原基础上加入了一些常用功能

### 预览

[hfanss.com](hfanss.com)

![在这里插入图片描述](https://blog-1252958858.file.myqcloud.com/2019/03/demo1.png#pic_center)

## 使用

### 下载主题

> [https://gitee.com/iyohei/material-plus](https://gitee.com/iyohei/material-plus)

### 安装
>git clone https://gitee.com/iyohei/material-plus.git 

```
下载到themes文件夹
剪切内部文件夹default下的 所有内容-source文件夹、_config.yml、package.json至博客根目录
打开命令行执行以下命令：
npm update
```
### 详细说明

所有配置均在博客根目录下config.yml中进行

内部所有配置均有中文说明，以下仅特别强调几点

1.文章页标签

```
---
title: 博文标题
date: 2019-03-31 15:54:38  #书写日期+时间
tags: 	#标签
- hexo主题
- material-x优化版
- material-plus
categories: #分类
- hexo
img: https://blog-1252958858.file.myqcloud.com/2019/03/material-plus.png #博文封面。本地图片显示方式为  /img/***.jpg 
newimg: true    #是否显示  new 标签
zhailu: 基于material-x主题魔改的hexo主题，material-plus主题，增添了部分功能，集成统计，广告。。。。。  #文章摘录。最少70字，否则封面会显示错乱
comments: false   #是否开启评论，默认true
toc: false     #是否显示目录，可在config.yml中统一配置
---
```

2.DIY

```
留言板		 /source/comment/index.md
友链		 /source/links/index.md
关于博主	     /source/about2/index.md
关于本站	     /source/about/index.md
logo、图标    /source/img  ##直接替换即可
```

就说这么多吧，暂时也想不起太多，在使用中遇到问题，也可在下面留言咨询
