[中文](https://gitee.com/iyohei/material-plus/blob/master/README.en.md)

## Theme Introduction

This topic is based on[ \[material-x\]](https://xaoxuu.com/wiki/material-x/)，Theme Magic Change, Original Author [Xiaowu Blog](https://www.wushile.top/), open sourced with the author's consent. This version has added some commonly used functions on the original basis

### Preview

[hfanss.com](hfanss.com)

![在这里插入图片描述](https://blog-1252958858.file.myqcloud.com/2019/03/demo1.png#pic_center)


## Use

### Download Theme

> [ https://gitee.com/iyohei/material-plus ]( https://gitee.com/iyohei/material-plus )

### Installation
>git clone  https://gitee.com/iyohei/material-plus.git  

```
Download to themes folder
Cut all the contents of the default folder - source folder,_config.yml, package.json to the root directory of the blog
Open the command line and execute the following command:
npm update
```
### Detailed explanation

All configurations are made in the config. yml directory at the root of the blog

All internal configurations are explained in Chinese, and only a few points are emphasized below

1. Article page tags

```
---
Title: Blog Title
Date: March 31, 2019 15:54:38 # Write date+time
Tags: # tags
-Hexo Theme
-Material-x optimized version
- material-plus
Categories: # Categories
- hexo
img:  https://blog-1252958858.file.myqcloud.com/2019/03/material-plus.png #Cover of the blog post. The local image display format is/img/* * *. jpg
Newimg: true # Whether to display the new tag
Zhailu: Hexo theme modified based on material-x theme, material plus theme, added some functions, integrated statistics, advertising..... #Excerpts from the article. At least 70 words, otherwise the cover will display confusion
Comments: false # Whether to enable comments, default to true
Toc: false # Whether to display the directory can be uniformly configured in config. yml
---
```

2.DIY

```
Message board			/source/comment/index. md
Friendship link			/source/links/index.md
About blogger			/source/bout2/index.md
About our website		/source/about/index. md
logo、 Icon				/source/img # # can be replaced directly
```

That's all for now. I can't remember too much. If you encounter any problems during use, you can also leave a message below for consultation

