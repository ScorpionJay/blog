title: java_web_http
date: 2015-10-10 11:03:54
tags:
- web
---

java web programmer
<!--more-->
http

service

servlet

jsp

tomcat

framework


---
ServerSocket
http://blog.csdn.net/lin49940/article/details/4398364

servlet 3 注解功能 
@WebServlet(value="/HelloServlet")

方案一：激活Tomcat的defaultServlet来处理静态文件

	<servlet-mapping>  
	    <servlet-name>default</servlet-name> 
	    <url-pattern>*.jpg</url-pattern>    
	</servlet-mapping>   
	<servlet-mapping>      
	    <servlet-name>default</servlet-name>   
	    <url-pattern>*.js</url-pattern>   
	</servlet-mapping>   
	<servlet-mapping>       
	    <servlet-name>default</servlet-name>      
	    <url-pattern>*.css</url-pattern>     
	</servlet-mapping>

Servlet中的过滤器Filter详解
http://www.oschina.net/question/565065_86538
三个有用的过滤器
http://www.iteye.com/topic/185094

多个过滤器问题
先写的先执行
使用注解并没有这么个参数，可以通过文件名入手。