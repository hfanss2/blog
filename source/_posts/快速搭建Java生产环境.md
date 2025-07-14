---
title: 快速搭建Java生产环境
date: 2019-03-10 16:26:38
tags: 
- Java生产环境
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/050.jpg
newimg: false
comments: true
zhailu: 本文指导开发者如何快速搭建一个Java生产环境，适用于windows系统下的使用
---
（本文使用于有一定基础的编程人员，如果小白的话请仔细，一步一步按照本文来 也可配置成功，有问题可在下方评论）

## 1. JDK

看好自己电脑的版本  X32/X64，然后下载一个版本。并不是越新越好，一般都是1.5、1.7

官网 http://www.oracle.com/technetwork/java/index.html，官网有时候会卡

我在自己的网盘里分享了，https://pan.baidu.com/s/1mjmDTOW

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/051.jpg)

### 安装：

安装很简单，按照步骤一步一步来就好了，

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/052.jpg)

 

这里可以更改安装路径，需要的可以自己改

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/053.jpg)

这一步是安装JRE，JDK中是包含JRE的，所以可安装也可不安装

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/054.jpg)

### 环境变量：

右击我的电脑——>属性——>高级——>环境变量——>在系统变量中找到path.

点击新建——>变量名：JAVA_HOME，变量值：你的java所在路径，如这是我的安装路径：E:\Java\jdk1.7.0_21，这个值只要到这目录就差不多了，不要在后面加\bin等东西了。

双击path——>在最前面加这么个东西   %JAVA_HOME%\bin;   分号不能少，必须是英文的分号。

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/055.jpg)![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/055.jpg)

![]()

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/056.jpg)

如果还有不清楚的，请去我的网盘下载  详细文档，里面有非常详细的说明

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/057.jpg)

校验环境变量是否成功

快捷键win+R——>输入cmd——>输java

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/058.jpg)

出现下图内容证明 成功

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/059.jpg)

## 2. Tomcat

网盘:https://pan.baidu.com/s/1jKciScA

这个有点简单，全部点下一步就行，环境变量可配可不配

配的话 接上面 JDK的环境变量配置方法，名字为CATALINA_HOME，

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/060.jpg)

跟上面一样的方法添加到 Path中,他这个配环境变量的目的其实是可以单独启动，我们只需要在工具中启动就可以了，所以可不安装

## 3. Eclipse

官网地址https://www.eclipse.org/downloads/

相关使用及配置  详见我另一篇博客http://blog.csdn.net/q2158798/article/details/77184898里面有JDK,Tomcat在Eclipse里的相关配置

## 4. Svn

这里提供一个在线安装的

Eclipse里 点击 help-install from site -出来界面后，点击右边  add,

Name:svn

Location：http://subclipse.tigris.org/update_1.10.x

 ![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/061.jpg)

全部选上，点击下方Finish开始下载，东西不大，但服务器在国外，网速不好可能会卡

SVN导出项目报错的话  可以参考我的另一篇文章

http://blog.csdn.net/q2158798/article/details/74612930

 

## 5. 反编译工具

https://pan.baidu.com/s/1dL4mKY

非常小巧的一个工具，直接把jar包往里面拖就能看到了

 

## 6. 数据库方面

推荐使用Navicat，可以链接多个数据库，下载地址:http://www.cr173.com/soft/126934.html

用此工具链接 Oracle的方法  参考我的另一篇文章

http://blog.csdn.net/q2158798/article/details/78487405

