---
title: Thymeleaf模版中的取值
date: 2019-05-01 13:12:38
tags: 
- Tomcat
- SpringBoot
- Thymeleaf
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/009.jpg 
newimg: false
comments: true
zhailu: 最近在项目中使用到了springBoot自带的Thymeleaf模版，之前也没用过，研究了一下它的语法，在此记录下
---
最近在项目中使用到了springBoot自带的Thymeleaf模版，之前也没用过，研究了一下它的语法，在此记录下

js取model的值

```
<script th:inline="javascript">
    var message = [[${message}]];
    console.log(message);
</script>
```

页面取值

```
<a th:text="${name}"></a>
或者
<a th:value="${name}"></a>
```

循环取值

```
<tr th:each="article: ${articleList}"> 
    <td th:text="${article.title}"></td> 
    <td th:text="${article.name}"></td> 
    <td th:text="${article.vcTitle}"></td> 
    <td th:text="${article.read}"></td> 
    <td th:text="${article.author}"></td> 
</tr>
```