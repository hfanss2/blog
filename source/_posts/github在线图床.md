---
title: github在线图床
date: 2025-07-03 09:23:22
tags: 
- github图床
- 在线图床
- 在线github图床
- 免费图床
categories: 
- 免费图床
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/125.jpg
newimg: true
comments: true
zhailu: 利用github API制作的在线图床，信息保存在浏览器中，填上token，即可实现在线上传图片至自己的github仓库内
---

github做的图床，原理是利用github API实现的在线上传，就一个页面，css和js都是集成在页面，相关信息保存在浏览器缓存中，配置一下即可使用

效果演示：

<a href="https://pic.hfanss.com/" target="_blank">github在线图床</a>

打开网站填写下列信息

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/126.jpg)

github用户名：用户名

仓库名：做图床的专用仓库的名称

分支名称：分支名称

存储路径：上传到的目标仓库位置的路径，不填则上传到根目录，填一个不存在的则会新建，开头和结尾不需要/分割，

github访问令牌：token,没有的话可以点击创建令牌新建

点击保存配置是将配置保存在浏览器中，清除浏览器缓存后必须重新设置

上传成功后是这样，图片会重新命名，会默认返回jsdelivr的CDN地址，并且自动复制在剪切板，

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/127.jpg)

想要使用该图床需具备下面要求

1.一个专门用作图床的github仓库

随便创建一个就行，不用开启pages,专门用来做图床使用

2.创建1个github token

创建一个token,权限可以自己斟酌，小白可以全选上

3.在页面将信息保存即可使用

在网站填写信息保存，即可开启上传之旅



支持自定义，fork本项目至自己仓库，使用netlify部署，并搭配自定义域名即可实现自己的在线图床，参考文章：<a href="https://hfanss.com/2025/github%20pages%E4%BD%BF%E7%94%A8%E5%85%8D%E8%B4%B9cdn%E5%8A%A0%E9%80%9F-netlify" target="_blank">netlify加速github pages</a>

项目资源全部集成在html中，fork后可自行修改，比如利用cloud flare的数据库做成可登录的，或者设置密码只能本人使用

等等。。。相信广大网友的diy能力应该很强

项目地址：<a href="https://github.com/hfanss2/pic-upload" target="_blank">github地址</a>



