title: spring mvc interceptor
date: 2015-10-31 00:08:45
tags:
- java
- spring
- spring mvc
---
spring mvc 拦截器
<!--more-->

## spring-mvc.xml
~~~
<mvc:interceptors>  
    <!-- 使用bean定义一个Interceptor，直接定义在mvc:interceptors根下面的Interceptor将拦截所有的请求 -->  
    <!-- <bean class="com.wind.interceptor.TestInterceptor"/>  -->
     <!-- 定义在mvc:interceptor下面的表示是对特定的请求才进行拦截的 --> 
     <mvc:interceptor>  
        <mvc:mapping path="/hello/testJpa"/>  
        <bean class="com.wind.interceptor.TestInterceptor"/>  
    </mvc:interceptor>   
</mvc:interceptors>  
~~~

## java
~~~java
package com.wind.interceptor;

import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.springframework.web.servlet.HandlerInterceptor;
import org.springframework.web.servlet.ModelAndView;

public class TestInterceptor implements HandlerInterceptor{

	public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler)
			throws Exception {
		// TODO Auto-generated method stub
		System.out.println("PRE HANDLE");
		return true;
	}

	public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler,
			ModelAndView modelAndView) throws Exception {
		// TODO Auto-generated method stub
		System.out.println("POST HANDLE");
		
	}

	public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex)
			throws Exception {
		// TODO Auto-generated method stub
		System.out.println("AFTER COMPLETION");
	}

}

~~~