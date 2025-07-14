---
title: github pages使用免费CDN加速-netlify
date: 2025-07-01 11:31:22
tags: 
- github
- github pages
- github CDN
- github netlify
categories: 
- github pages
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/122.jpg
newimg: true
comments: true
zhailu: 使用github pages+netlify使用免费的CDN服务给博客网站进行加速，一键关联项目，自动部署，速度比较不错
---

github pages大家都知道，很多人用它来做个人博客，但是github pages在国内的访问速度很拉跨，经常访问不正常，对github pages加速的方式有很多种，今天介绍一下netlify，优点是，一键关联github项目，github更新，会自动部署，方便快捷，且免费，速度也很不错

Netlify是什么呢？

‌静态网站托管‌：Netlify专为HTML/CSS/JS等静态资源设计，支持主流前端框架（如React、Vue、Hugo等），无需服务器运维即可实现全球CDN加速。‌‌
1‌.自动化工作流‌：
集成GitHub/GitLab/Bitbucket仓库，代码推送后自动触发构建与部署。‌‌
2.提供自定义构建命令（如npm run build）和输出目录配置。‌‌
3‌.免费基础服务‌：
包含100GB月流量、300分钟构建时长及免费HTTPS证书。‌‌
4.提供*.netlify.app子域名，支持绑定自定义域名-注意：**不用备案！！！**

看看这介绍，是不是跟github pages特别搭配，100GB流量对于个人而言完全使用不完，如果把图片再单独拆出来，光文字资源来说，非常绰绰有余了。至于图床可以参考这个文章，也是免费的，[github图床使用CDN加速](https://hfanss.com/2025/github%20%E5%9B%BE%E5%BA%8A%E4%BD%BF%E7%94%A8%E5%85%8D%E8%B4%B9cdn%E5%8A%A0%E9%80%9F-jsdelivr)

## 一、部署github pages

静态博客怎么部署在github pages上就不多赘述，很多参考资料。

## 二、配置netlify

### 1.登录netlify

使用github账号登录 [netlify](https://app.netlify.com/)

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/107.jpg)

点击右侧新建项目-Add new project

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/108.jpg)

### 2.选择github仓库

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/109.png)

选择具体的仓库

第一个是选择netlify可用github所有仓库，第二个是选择netlify只能使用github指定的库，暂默认第二个我们github pages仓库即可

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/110.jpg)

### 3.部署

Team:默认项目名

project name:默认项目名，也可自定义，建议项目名，影响生成的默认域名

往下拉：

branch to deploy: main   部署分支，github默认main分支，可以改其他

剩余的可不用填

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/111.jpg)

点击最下面 Deploy 项目名

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/112.jpg)

部署成功后显示下图

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/113.jpg)

点击图中标识1的位置，可以简单预览下，没问题的话就可以了

到这一步其实已经结束了，但是有自定义域名的可以继续往下看

### 4.自定义域名

点击上图中标识2的位置，右侧点击Add a domin-Add a domain you already own（添加一个已经拥有的域名）

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/115.jpg)

点击验证 verify

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/116.jpg)

然后会让你去验证域名，因为我已经验证过了，所以没法截图，大概意思就是让你在域名提供商那里去首先验证下该域名是自己的，需要添加个一串数值指向到子域名，参考下图

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/117.jpg)

验证好之后，就直接将域名指向它指定的地址就等待就行了，参考下图

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/118.jpg)

验证好之后是这样的，参考下图，就是红框内没有验证DNS的字样，并且左边域名也变绿就可以了

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/119.jpg)

至于https的ssl证书，有netlify自动配置，刚添加完域名后，它会自动配置ssl证书，参考下图

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/120.jpg)

上图这种就是正在配置证书，时间可能久一点，需要10-20分钟左右

配置证书成功后是这样的，显示对号就是OK的，下面domains那里就是对应的自己的自定义域名，时间是3个月，但是到期后它会自动续发ssl证书，不用担心。

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/121.jpg)

OK，大功告成，现在就可以大胆的访问，不用担心github pages访问不正常的情况了