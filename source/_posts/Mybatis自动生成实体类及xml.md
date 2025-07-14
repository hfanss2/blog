---
title: Mybatis自动生成实体类及xml
date: 2019-06-17 21:43:22
tags: 
- Java
- Mybatis
- mybatis-generator
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/026.jpg
newimg: false
zhailu: 开发中经常都是现有数据字典，再建表开发的情况，很少有现有java文件再有表的情况，那么在这个时候，一个简便的根据表生成java文件的代码便有了
---
> Mybatis自动生成实体类及xml

如果自己根据表手动生成需要的java文件无疑是非常麻烦的，在公司用的是自己写的一段代码生成，比较复杂，代码量也非常大，这几天刚好做一个boot的小demo，于是把mybatis的generator自动生成工具使用整理记录下

1.引入jar包-pom.xml

```
<dependencies>
	<!-- ..... -->
    <!-- mysql驱动 -->
    <dependency>
        <groupId>mysql</groupId>
        <artifactId>mysql-connector-java</artifactId>
        <version>5.1.35</version>
    </dependency>
    <!-- mysql自动生成实体类-->
    <dependency>
        <groupId>org.mybatis.generator</groupId>
        <artifactId>mybatis-generator-core</artifactId>
        <version>1.3.5</version>
    </dependency>
<dependencies>
```

2.resources文件夹下增加mybatis-generator.xml文件

```
<?xml version="1.0" encoding="UTF-8"?> <!DOCTYPE generatorConfiguration   PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"   "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
<generatorConfiguration>
	<context id="DB2Tables" targetRuntime="MyBatis3Simple">
		<commentGenerator>
			<property name="suppressDate" value="true" />                 
			<!-- 是否去除自动生成的注释 true：是 ： false:否 -->
			<!-- 这个注释是generator的注释。不是建表时手输的，没什么卵用-->
			<property name="suppressAllComments" value="true" />
		</commentGenerator>          		
		<!--数据库链接URL，用户名、密码 -->
		<jdbcConnection driverClass="com.mysql.jdbc.Driver"
			connectionURL="jdbc:mysql://localhost:3306/hfanss?characterEncoding=utf-8"
			userId="root" password="123456">
		</jdbcConnection>
		<javaTypeResolver>
			<property name="forceBigDecimals" value="false" />
		</javaTypeResolver> 		
		<!-- 设置Java类生成的位置 -->
		<javaModelGenerator targetPackage="com.hfanss.blog.VO"
			targetProject=".\src\main\java">
			<property name="enableSubPackages" value="true" />
			<property name="trimStrings" value="true" />
		</javaModelGenerator> 				
		<!-- 生成映射文件的包名和位置 ***mapper.xml-->
		<sqlMapGenerator targetPackage="\spring\sqlMap"
			targetProject=".\src\main\resources">
			<property name="enableSubPackages" value="true" />
		</sqlMapGenerator> 				
		<!-- 生成DAO的包名和位置 ***mapper.java-->
		<javaClientGenerator type="XMLMAPPER"
			targetPackage="com.hfanss.blog.dao" targetProject=".\src\main\java">
			<property name="enableSubPackages" value="true" />
		</javaClientGenerator> 		
		<!-- 所有要生成的表名 -->
		<table tableName="info"></table>
		<table tableName="article"></table>
		<table tableName="comments"></table>
		<table tableName="links"></table>
		<table tableName="menus"></table>
		<table tableName="notice"></table>
		<table tableName="articleSort"></table>
	</context>
</generatorConfiguration>
```

3.执行、GetAutoEntityAndDao放在src/test/java文件夹下,右键Aun as

```
/**
 * 功能描述:自动生成mapper.xml、dao、entity
 * @author: hfanss
 * @date: 2019年6月17日 下午8:25:55 
 */
public class GetAutoEntityAndDao {

	// 该配置文件放在src\\main\\resources\\该路径下即可
	public static void main(String[] args) {
		args = new String[] { "-configfile", "src\\main\\resources\\mybatis-generator.xml", "-overwrite" };
		ShellRunner.main(args);
	}

}
```

问题：实体类没有注释，十分不方便。

看了下源码。嗯，如果不改源码是不能实现生成自定义注释的。改天有时间再研究下！

附上项目及文件位置截图

![](https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/027.jpg)

