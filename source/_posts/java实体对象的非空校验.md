---
title: java实体对象的非空校验
date: 2021-7-12 19:31:22
tags: 
- Java
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/005.jpg
newimg: false
comments: true
zhailu: 工作中遇到针对API中存在的实体类的非空校验，写了个通用工具类，通过反射去实现效果
---

工作中遇到针对API中存在的实体类的非空校验，如果不封装只能一个一个获取再校验。比较麻烦，所以写了个通用工具类，通过反射去实现效果

```java
/**
	 * 功能描述:对象非空校验
	 * 
	 * @author: hfanss
	 * @date: 2021-07-12 6:52:11 PM
	 */
	public void vaildate(Object vo, List<String> parms)
	{
		Field[] fields = vo.getClass().getDeclaredFields();
		try
		{
			for (String validName : parms)
			{
				for (Field fi : fields)
				{
					fi.setAccessible(true);// 打开私有属性，否则只能获取到共有属性
					String name = fi.getName();// 获取属性名称
					if (!validName.equals(name))
						continue;
					String value = fi.get(vo) == null ? "" : fi.get(vo).toString();
					if (StringUtils.isBlank(value))
					{
						System.out.println("参数：{"+name+"}值为空");
						break;
					}
				}
			}
		} catch (IllegalArgumentException | IllegalAccessException e)
		{
			// 记录日志
			System.out.println("校验对象失败：{" + vo + "},异常信息：{" + e + "}");
		}
	}
```
调用方式

```java
@Test
	public void main()
	{
		TestVO vo = new TestVO();

		vo.setId(1);
//		vo.setName("hfanss");
		vo.setSf("111");
		List<String> parms = Arrays.asList("name", "number");
		vaildate(vo, parms);

	}
```
实体类参数

```java
	private int id;
	private String name;
	private String number;
	private String sf;
	public int getId()
	{
		return id;
	}
	public void setId(int id)
	{
		this.id = id;
	}
	................................
```
测试结果

```java
控制台输出  
参数：{name}值为空
参数：{number}值为空
```

代码地址 ： [点我](https://gitee.com/iyohei/hfanssutils/blob/master/src/main/java/com/hfanss/utils/EntityUtils.java)