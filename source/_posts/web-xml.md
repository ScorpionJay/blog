title: web.xml
date: 2015-09-15 13:48:59
tags:
- java
- web
---

web.xml配置
<!--more-->
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns="http://xmlns.jcp.org/xml/ns/javaee"
	xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd"
	id="WebApp_ID" version="3.1">
	
	<!-- web应用的名称 -->
	<display-name>testweb</display-name>
	
	<!-- 描述 -->
	<description>this is a test web project</description>
	
	<!-- 默认页面 -->
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
	</welcome-file-list>
	
	<!-- 错误页面 error-code表示错误码 location 对应的页面 -->
	<error-page>
		<error-code>404</error-code>
		<location>/404.html</location>
	</error-page>
	<error-page>
		<error-code>500</error-code>
		<location>/500.html</location>
	</error-page>
	
	<!-- session -->
	<session-config>
		<session-timeout>360000</session-timeout>
	</session-config>
	
	
	<!-- servlet 过滤器 监听器配置 -->
	
	
	
</web-app>

~~~
