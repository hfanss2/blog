---
title: JDBC链接数据库
date: 2018-12-25 20:29:38
tags: 
- Java
categories: 
- Java
img:   https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/032.jpg
newimg: false
zhailu: 在Java开发中使用最原始的JDBC链接数据库，最简单的java链接数据库代码呈现，驱动-获得链接-获得Statement-链接-获取
---
> 学习记录：复习
>
> JDBC简单链接数据库

```
/**    关闭资源用*/
Connection conn = null;
Statement stmt = null;
ResultSet rest = null;
/**设置url,user,password,sql*/
String url = "jdbc:mysql://localhost:3306/kevin?useUnicode=true&characterEncoding=utf-8";
String user = "root";
String password = "123456";
String sql = "select * from blog";
try
{
// 注册驱动
Class.forName("com.mysql.jdbc.Driver");
// 获得数据库链接
conn = DriverManager.getConnection(url, user, password);
// 获得Statement
stmt = conn.createStatement();
rest = stmt.executeQuery(sql);
while (rest.next())
{
System.out.println(rest.getString("title") + "_" + rest.getString("viceTitle"));
}
} catch (Exception e)
{
System.err.println("发生异常："+e);
} finally
{//关闭资源
rest.close();
stmt.close();
conn.close();
}
```

关闭资源放在finally中

需引入mysql-connector-java-***.jar，如果没有使用maven可在[官网下载](https://cdn.mysql.com//Downloads/Connector-J/mysql-connector-java-5.1.47.zip)或 [我的网盘](https://pan.baidu.com/s/1_xQ_KfLhJ7skTJDfK5V8vg#list/path=%2Fjava%2Fmysql&parentPath=%2Fjava)

[![QQ图片20180919200826.jpg](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/033.jpg)](javascript:void(0);)
