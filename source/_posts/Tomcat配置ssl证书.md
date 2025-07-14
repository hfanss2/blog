---
title: Tomcat配置ssl证书
date: 2019-01-10 20:29:38
tags: 
- Java
categories: 
- Tomcat
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/036.jpg
newimg: false
comments: true
zhailu: 最近搞这个https搞的头疼，百度下载的ssl证书没有密码，纠结了很久.特开贴记录一下，希望后来的同学们少走点弯路
---
最近搞这个https搞的头疼，百度下载的ssl证书没有密码，纠结了很久

特开贴记录一下，希望后来的同学们少走点弯路

## 下载证书

这里以百度云为例（网上阿里的有很多教程，这里就不多赘述）

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/037.jpg)](javascript:void(0);)

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/038.jpg)](javascript:void(0);)

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/039.jpg)](javascript:void(0);)

这个密码就是证书的密码，起初我一直以为就是解压密码，最后问过百度客服才知道就是证书密码

## 配置tomcat

1.将下载下来的后缀为jks的证书放入tomcat的conf目录下

2.打开该目录下的server.xml，添加以下内容

```
<Connector port="443" protocol="org.apache.coyote.http11.Http11NioProtocol" maxThreads="150" SSLEnabled="true" scheme="https" secure="true" keystoreFile="证书绝对路径" keystorePass="证书密码" clientAuth="false" sslProtocol="TLS" />
```

另外修改原有内容

```
<Connector port="8080" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="8443" />
<Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
```

修改为

```
<Connector port="80" protocol="HTTP/1.1"
               connectionTimeout="20000"
               redirectPort="443" />
<Connector port="8009" protocol="AJP/1.3" redirectPort="443" />
```

OK后，重启下tomcat，进入<https://localhost>会跳转到<https://localhost>

[![img](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/040.jpg)](javascript:void(0);)

## 如果部署的是java web项目，还需要以下配置

tomcat/conf/server.xml

```
<Context path="/" reloadable="true" docBase="项目绝对路径" />    
```

web项目的web.xml中还需要更改（包含在根标签内，</web-app>之上）

```
<!-- 跳转https -->  
    <security-constraint>  
         <web-resource-collection >  
            <web-resource-name >SSL</web-resource-name>  
            <url-pattern>/*</url-pattern>  
        </web-resource-collection>  
        <user-data-constraint>  
            <transport-guarantee>CONFIDENTIAL</transport-guarantee>  
        </user-data-constraint>  
    </security-constraint>
```

此配置目的：将所有请求转为https

OK，大功告成，重启tomcat，访问localhost就可以看到效果了