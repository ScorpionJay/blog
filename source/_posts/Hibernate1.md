title: Hibernate1
date: 2015-08-28 13:49:49
tags:
- hibernate
---

Hibernate是一个开放源代码的对象关系映射框架，它对JDBC进行了非常轻量级的对象封装，使得Java程序员可以随心所欲的使用对象编程思维来操纵数据库。
<!--more-->

hibernate 
	配置
	工程模式
	实体类 mapping 数据库中的表
	使用JDBC是手动去转换


使用Maven构将 pom.xml文件
~~~XML
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>

	<groupId>hibernate</groupId>
	<artifactId>hibernate</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>jar</packaging>

	<name>hibernate</name>
	<url>http://maven.apache.org</url>

	<properties>
		<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	</properties>

	<dependencies>

		<dependency>
			<groupId>org.hibernate</groupId>
			<artifactId>hibernate-core</artifactId>
			<version>5.0.0.Final</version>
		</dependency>

		<dependency>
			<groupId>mysql</groupId>
			<artifactId>mysql-connector-java</artifactId>
			<version>5.1.36</version>
		</dependency>

		<dependency>
			<groupId>junit</groupId>
			<artifactId>junit</artifactId>
			<version>4.12</version>
		</dependency>
	</dependencies>
</project>

~~~


----------


hibernate配置文件 hibernate.cfg.xml src/main/resources 路径下
~~~xml
<?xml version='1.0' encoding='utf-8'?>
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

	<session-factory>

		<!-- Database connection settings -->
		<property name="connection.driver_class">com.mysql.jdbc.Driver</property>
		<property name="connection.url">jdbc:mysql://localhost:33060/test</property>
		<property name="connection.username">root</property>
		<property name="connection.password">root</property>

		<!-- JDBC connection pool (use the built-in) -->
		<property name="connection.pool_size">1</property>

		<!-- SQL dialect -->
		<property name="dialect">org.hibernate.dialect.MySQLDialect</property>

		<!-- Enable Hibernate's automatic session context management -->
		<property name="current_session_context_class">thread</property>

		<!-- Disable the second-level cache -->
		<property name="cache.provider_class">org.hibernate.cache.internal.NoCacheProvider</property>

		<!-- Echo all executed SQL to stdout -->
		<property name="show_sql">true</property>

		<!-- Format SQL -->
		<property name="format_sql">true</property>

		<!-- Drop and re-create the database schema on startup -->
		<property name="hbm2ddl.auto">update</property>

		<mapping resource="com/hibernate/entity/User.hbm.xml" />

	</session-factory>

</hibernate-configuration>
~~~

----------


User.java
~~~java
package com.hibernate.entity;

import java.util.Date;

/**
 * @author Jay
 */
public class User {
	private int id;
	private String name;
	private Date birthday;

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public Date getBirthday() {
		return birthday;
	}

	public void setBirthday(Date birthday) {
		this.birthday = birthday;
	}

}
~~~

----------

User映射配置文件 src/main/resources/com.hibernate.entity 路径下
~~~xml
<hibernate-mapping package="com.hibernate.entity">

    <class name="User" table="User">
        <id name="id" column="user_id"/>
        <property name="name"/>
        <property name="birthday"/>
    </class>

</hibernate-mapping>
~~~

----------

测试
~~~java
package com.hibernate;

import java.util.Date;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.hibernate.entity.User;

/**
 * @author Jay
 */
public class UserTest {
	public static void main(String[] args) {
		
		Configuration conf = new Configuration();
        //加载主配置
        conf.configure("/hibernate.cfg.xml");
        //获取SessionFactory
        SessionFactory sf = conf.buildSessionFactory();
        //获取Session
        Session session = sf.openSession();
        //开启事务
        Transaction transction = session.beginTransaction();
        //执行添加操作
        User user = new User();
        user.setId(5);
        user.setName("Jay");
        user.setBirthday(new Date());
        session.save(user);
        //提交事务
        transction.commit();
        //关闭session
        session.close();
	}

}
~~~

----------

参考：
	1.http://docs.jboss.org/hibernate/orm/5.0/manual/en-US/html/ch01.html#