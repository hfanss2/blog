---
title: SpringBoot实现拦截器
date: 2019-06-25 21:52:22
tags: 
- springBoot
- 拦截器
categories: 
- Java
img:  https://gcore.jsdelivr.net/gh/hfanss2/githubpic@master/blog/010.jpg 
newimg: false
comments: true
zhailu: 在项目中实现拦截器是最基本的功能，之前用的框架都是spring+mvc，最近用了boot，特此开帖记录下使用方法
---

首先，你的项目要能跑起来，且基于springboot的

boot的拦截器不用配置web.xml，按照特定名字书写，它会自动识别（位置随便放，只要在代码目录下就可以）

1.拦截器  SessionInterceptor.java 

```
package com.hfanss.blog.utils;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

/**
 * 功能描述:拦截器实现类
 * @author: hfanss
 * @date: 2019年6月25日 下午9:23:32 
 */
public class SessionInterceptor implements HandlerInterceptor
{

	@Override
	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception
	{
		System.err.println("拦截器进来了,路径为："+request.getRequestURI());
		if (request.getRequestURI().equals("/admin/**"))
		{
			//TODO  验证登录token
			return true;
		}else {
			
			return true;
		}
	}

	@Override
	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception
	{
		// TODO Auto-generated method stub

	}

	@Override
	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception
	{
		// TODO Auto-generated method stub

	}

}
```

2.路径 SessionConfiguration.java

```
package com.hfanss.blog.utils;

import java.util.List;

import org.springframework.context.annotation.Configuration;
import org.springframework.format.FormatterRegistry;
import org.springframework.http.converter.HttpMessageConverter;
import org.springframework.validation.MessageCodesResolver;
import org.springframework.validation.Validator;
import org.springframework.web.method.support.HandlerMethodArgumentResolver;
import org.springframework.web.method.support.HandlerMethodReturnValueHandler;
import org.springframework.web.servlet.HandlerExceptionResolver;
import org.springframework.web.servlet.config.annotation.AsyncSupportConfigurer;
import org.springframework.web.servlet.config.annotation.ContentNegotiationConfigurer;
import org.springframework.web.servlet.config.annotation.CorsRegistry;
import org.springframework.web.servlet.config.annotation.DefaultServletHandlerConfigurer;
import org.springframework.web.servlet.config.annotation.InterceptorRegistry;
import org.springframework.web.servlet.config.annotation.PathMatchConfigurer;
import org.springframework.web.servlet.config.annotation.ResourceHandlerRegistry;
import org.springframework.web.servlet.config.annotation.ViewControllerRegistry;
import org.springframework.web.servlet.config.annotation.ViewResolverRegistry;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

/**
 * 功能描述:配置拦截器路径 /admin/
 * @author: hfanss
 * @date: 2019年6月25日 下午9:37:21 
 */
@Configuration
public class SessionConfiguration implements WebMvcConfigurer
{
	
	@Override
	public void addInterceptors(InterceptorRegistry registry)
	{
		registry.addInterceptor(new  SessionInterceptor()).addPathPatterns("/admin/**");
		
	}
	.....
}
```

运行项目，拦截器实现类方法内打个断点，会发现所有带 admin的路径都会被拦截到

可以根据需要定义拦截的路径，拦截器常用的功能也就用户登录控制
