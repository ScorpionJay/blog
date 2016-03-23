title: spring mvc
date: 2015-09-18 10:12:29
tags:
- java
- spring
- spring mvc
---

spring mvc学习笔记
<!--MORE-->

# 配置

## web.xml
~~~xml
<!--配置dispatchServlet -->
<servlet>
	<servlet-name>DispatcherServlet</servlet-name>
	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
	<init-param>
		<param-name>contextConfigLocation</param-name>
		<param-value>WEB-INF/spring-mvc.xml</param-value>
	</init-param>
	<load-on-startup>1</load-on-startup>
</servlet>
<servlet-mapping>
	<servlet-name>DispatcherServlet</servlet-name>
	<url-pattern>/</url-pattern>
</servlet-mapping>
~~~

## spring-mvc.xml
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context 
        http://www.springframework.org/schema/context/spring-context.xsd
        http://www.springframework.org/schema/mvc
        http://www.springframework.org/schema/mvc/spring-mvc.xsd">

	<context:annotation-config />

	<mvc:annotation-driven />

	<context:component-scan base-package="com.wind.controller" />

	<!-- 使用默认的Servlet来响应静态文件 -->
	<mvc:default-servlet-handler />


	<!-- 配置ViewResolver。 可以用多个ViewResolver。 使用order属性排序。 InternalResourceViewResolver放在最后。 -->
	<mvc:annotation-driven>
		<mvc:message-converters register-defaults="true">
			<bean class="org.springframework.http.converter.json.MappingJackson2HttpMessageConverter"/>
		</mvc:message-converters>
	</mvc:annotation-driven>


<mvc:interceptors>  
    <!-- 使用bean定义一个Interceptor，直接定义在mvc:interceptors根下面的Interceptor将拦截所有的请求 -->  
    <!-- <bean class="com.wind.interceptor.TestInterceptor"/>  -->
     <!-- 定义在mvc:interceptor下面的表示是对特定的请求才进行拦截的 --> 
     <mvc:interceptor>  
        <mvc:mapping path="/hello/testJpa"/>  
        <bean class="com.wind.interceptor.TestInterceptor"/>  
    </mvc:interceptor>   
</mvc:interceptors>  


</beans>
~~~

## controller
~~~java
package com.wind.controller;

import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.wind.service.iface.IHelloService;

@RestController
@RequestMapping(value="hello")
public class HelloCtrl {

	private static final Logger logger = LoggerFactory.getLogger(HelloCtrl.class);
	
	@Autowired
	IHelloService helloService;
	
	@RequestMapping(value="test")
	private String test() {
		String str = helloService.test();
		logger.info(str + " controller");
		return str;
	}
	
}
~~~


# 问题
## 返回值乱码问题
~~~xml
<mvc:annotation-driven>
        <mvc:message-converters>
            <bean class="org.springframework.http.converter.StringHttpMessageConverter">
                <property name="supportedMediaTypes">
                    <list>
                        <value>text/plain;charset=UTF-8</value>
                        <value>text/html;charset=UTF-8</value>
                    </list>
                </property>
            </bean>
        </mvc:message-converters>
</mvc:annotation-driven>
~~~
