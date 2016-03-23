title: spring mybatis
date: 2015-10-31 00:09:35
tags:
- spring
- mybatis
---
spring mybatis集成
<!--more-->

## pom
~~~xml
<!-- mybatis -->
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis</artifactId>
	<version>3.3.0</version>
</dependency>
<dependency>
	<groupId>org.mybatis</groupId>
	<artifactId>mybatis-spring</artifactId>
	<version>1.2.3</version>
</dependency>
~~~

## java
~~~java
package com.wind.repository.mybatis;

import java.util.List;

import com.wind.entity.jpa.User;


public interface UserRepository {
	
	List<User> find();
	
	void save(User user);
	
}
~~~

## mapper.xml
~~~xml
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" 
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.wind.repository.mybatis.UserRepository">


	<select id="find" resultType="com.wind.entity.jpa.User">
		select 
        	id 									id, 
        	name 								name 
        from 
             user
	</select>
	
	<insert id="save" parameterType="com.wind.entity.jpa.User">
		insert into user(name) values(#{name})
	</insert>
	
	
</mapper> 

~~~

## entity
~~~java
package com.wind.entity.jpa;

import java.io.Serializable;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "user")
public class User implements Serializable {
	private static final long serialVersionUID = -2509439493563083804L;

	@Id
	@GeneratedValue(strategy = GenerationType.AUTO)
	@Column(name = "id")
	private Integer id;

	@Column(name = "name")
	private String name;

	public Integer getId() {
		return id;
	}

	public void setId(Integer id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public User(String name) {
		super();
		this.name = name;
	}

	@Override
	public String toString() {
		return "Hello [id=" + id + ", name=" + name + "]";
	}

	public User() {
		super();
	}

}
~~~

## applicationContext-mybatis.xml
~~~xml
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p="http://www.springframework.org/schema/p"  
    xmlns:context="http://www.springframework.org/schema/context"  
    xmlns:mvc="http://www.springframework.org/schema/mvc"  
    xsi:schemaLocation="http://www.springframework.org/schema/beans    
                        http://www.springframework.org/schema/beans/spring-beans.xsd    
                        http://www.springframework.org/schema/context    
                        http://www.springframework.org/schema/context/spring-context.xsd    
                        http://www.springframework.org/schema/mvc    
                        http://www.springframework.org/schema/mvc/spring-mvc.xsd">  
    <!-- 自动扫描 -->  
    <context:component-scan base-package="com.wind.repository.mybatis" />  
<!--     引入配置文件  
    <bean id="propertyConfigurer"  
        class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">  
        <property name="location" value="classpath:META-INF/jdbc.properties" />  
    </bean>   -->
    
    <!-- 配置DataSource数据源 -->
    <bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
        <property name="url" value="jdbc:mysql://localhost:3306/wind"/>
        <property name="username" value="root"/>
        <property name="password" value="123456"/>
    </bean>
    
  
<!--     <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource"  
        destroy-method="close">  
        <property name="driverClassName" value="${driver}" />  
        <property name="url" value="${url}" />  
        <property name="username" value="${username}" />  
        <property name="password" value="${password}" />  
        初始化连接大小  
        <property name="initialSize" value="${initialSize}"></property>  
        连接池最大数量  
        <property name="maxActive" value="${maxActive}"></property>  
        连接池最大空闲  
        <property name="maxIdle" value="${maxIdle}"></property>  
        连接池最小空闲  
        <property name="minIdle" value="${minIdle}"></property>  
        获取连接最大等待时间  
        <property name="maxWait" value="${maxWait}"></property>  
    </bean>   -->
  
    <!-- spring和MyBatis完美整合，不需要mybatis的配置映射文件 -->  
    <bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean">  
        <property name="dataSource" ref="dataSource" />  
        <!-- 自动扫描mapping.xml文件 -->  
        <property name="mapperLocations" value="classpath*:/META-INF/mybatis/*.xml"></property>  
    </bean>  
  
    <!-- DAO接口所在包名，Spring会自动查找其下的类 -->  
    <bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">  
        <property name="basePackage" value="com.wind.repository.mybatis" />  
        <property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"></property>  
    </bean>  
  
    <!-- (事务管理)transaction manager, use JtaTransactionManager for global tx -->  
    <bean id="transactionManager"  
        class="org.springframework.jdbc.datasource.DataSourceTransactionManager">  
        <property name="dataSource" ref="dataSource" />  
    </bean>  
  
</beans>  
~~~