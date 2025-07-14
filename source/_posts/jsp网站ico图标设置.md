---
title: jsp网站ico图标设置
date: 2018-12-25 20:29:38
tags: 
- Java
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/028.jpg
newimg: false
zhailu: 学习记录-小技巧，在Java开发web网站中设置ico图标，ico图标放在webapp下，在JSP页面引入图标
---
> 学习记录：小技巧
>
> web项目中设置ico图标

> ico图标放在webapp下

在jsp页面中引入（ps:每个jsp都要引入,最好放在header或者footer既头部或尾部页面中，可以做到一处引用，多处使用）

```
<!--  网站图标 --><link rel="shortcut icon" href="../static/img/favicon.ico">
```

[![QQ图片20181024210453.jpg](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/029.jpg)](javascript:void(0);)

各位可根据目录结构和引入地址适当更改