---
title: 初识Python-99乘法表
date: 2019-10-20 14:50:22
tags: 
- Python
- 99乘法表
categories: 
- Python
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/008.jpg 
newimg: false
comments: true
zhailu: 都说人生苦短，要用python，听说有些省市还将此语言列为小学计算机课程，今天也来尝试下
---

python的份额一年比一年多，今天也来体验下

## 1.安装

网上教程很多，随便推荐一篇吧，老廖的

https://www.liaoxuefeng.com/wiki/1016959663602400/1016959856222624

## 2.上手

因为我是做java开发的，所以使用的IDE是sts,安装了一下插件

https://blog.csdn.net/qq_36955890/article/details/93191243

## 3.体验

来个99乘法表吧

```
# -*- coding:utf-8 -*-
'''
@note:
@author: hfanss
@date: 2019/10/20 14:27:27

'''
#打印一个简单的99乘法表
#外层循环  控制左边1-9
for i in range(1,10):
    #内层循环控制 右边1-9
    for j in range(1,i+1):
        #print("{0}*{1}={2}".format(i,j,i*j),end = " ")
        print("{0}*{1}={k}".format(i,j,k=i*j),end = " ")
    print()
```

完美打印

## 4.随想

简单来说，python的语法相对来说更简洁些，一些常用的操作做了简化，比如说键盘录入，只需要input()可以了，java中很麻烦

输出的时候也做了一些定制，上面打印99乘法表的时候就可以看出来了



嗯，简单体验下，有时间再继续学下去