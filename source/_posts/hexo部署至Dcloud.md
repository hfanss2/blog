---
title: hexo部署至Dcloud
date: 2020-08-09 11:14:22
tags: 
- 技术
- hexo部署
- Dcloud
categories: 
- hexo
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/015.jpg
newimg: false
comments: true
zhailu: 新发现一个部署hexo的好地方，且自带CDN，完全免费，操作也异常简单，发帖共享下
---

先放上官方简介

https://uniapp.dcloud.io/uniCloud/hosting?id=%e7%ae%80%e4%bb%8b

具体步骤大致说一下

1.申请uniCloud账号

2.创建服务空间

3.下载HBuilderX ，并登陆刚才的账号

4.选中你本地的hexo生成后的public文件夹

5.右键点击发行-上传到网站服务器

6.网站打开刚才创建的服务空间

左侧点击前端网页托管，右侧点击参数管理

这里可以配置自定义域名、添加证书

注意事项：

1.发行的时候，它会提示你是否替换源文件，这里建议全部替换，因为不管你是修改老文件还是新增文件都会涉及到原来文件，不过这里说一下，它的速度很慢，文件少就快，文件多就慢，你也可以选择在web控制台上传，那个会很快

2.既然免费就会有一定的不足，它最大的不足就是不主动提供https服务，即使你提供了https证书

当然这里也有解决方式：修改index模版，位置在主题的layout根目录，一般名字为index.ejs，

打开后在最顶部加入如下代码，完美解决

```
 <script>
 var url = window.location.href; if(url.indexOf("localhost") < 0){if (url.indexOf("https") < 0) {url = url.replace("http:", "https:");window.location.replace(url);}}
</script>
```

3.还有最为诟病的一点，并非即时部署，发行完之后，大概会有5-10分钟的延时，不过可以接受

4.当然最主要的优点还是国内阿里云服务器，免费，自带CDN，操作简单

我个人备份了一个

[blog.hfanss.com](https://blog.hfanss.com/)

目前本站主站coding，副站dcloud，源代码部署在gitee上

有问题下方留言