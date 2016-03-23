title: spring el
date: 2015-11-09 15:56:17
tags:
- spring 
---
spring el配置
<!--more-->
## 读取配置文件
~~~xml
<bean id="propertyConfigurer" class="org.springframework.context.support.PropertySourcesPlaceholderConfigurer">
<property name="locations">
    <list>
      	<value>classpath:META-INF/database/*.properties</value>
    </list>
</property>
</bean>
~~~

## 配置文件
~~~xml
#connection mysql configure
database.driver=com.mysql.jdbc.Driver
database.url=jdbc:mysql://localhost:3306/wind?useUnicode=true&amp;characterEncoding=UTF-8
database.user=root
database.password=123456
database.minPoolSize=1
database.maxPoolSize=300
database.maxIdleTime=60
database.acquireIncrement=5
database.idleConnectionTestPeriod=60
~~~

## el使用
~~~xml
<bean id="mysqlDataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">  
<property name="driverClass" value="${database.driver}" />  
<property name="jdbcUrl" value="${database.url}" />  
<property name="user" value="${database.user}" />  
<property name="password" value="${database.password}" />  
<property name="minPoolSize" value="${database.minPoolSize}" />  
<property name="maxPoolSize" value="${database.maxPoolSize}" />  
<property name="maxIdleTime" value="${database.maxIdleTime}" />  
<property name="acquireIncrement" value="${database.acquireIncrement}" />  
<property name="idleConnectionTestPeriod" value="${database.idleConnectionTestPeriod}" />  
</bean>  
~~~

