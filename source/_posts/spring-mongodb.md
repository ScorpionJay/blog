title: spring mongodb
date: 2015-10-31 00:09:17
tags:
- spring
- mongodb
---
spring mongodb
<!--more-->

## applicationContext-mongo.xml
~~~ xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xmlns:tx="http://www.springframework.org/schema/tx" xmlns:jpa="http://www.springframework.org/schema/data/jpa"
	xmlns:mongo="http://www.springframework.org/schema/data/mongo"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
            http://www.springframework.org/schema/data/mongo
            http://www.springframework.org/schema/data/mongo/spring-mongo.xsd
            http://www.springframework.org/schema/context
            http://www.springframework.org/schema/context/spring-context.xsd
            http://www.springframework.org/schema/tx
            http://www.springframework.org/schema/tx/spring-tx.xsd
            http://www.springframework.org/schema/data/jpa
            http://www.springframework.org/schema/data/jpa/spring-jpa.xsd">


	<mongo:mongo id="mongo" host="localhost" port="27017">
		<mongo:options connections-per-host="8"
			threads-allowed-to-block-for-connection-multiplier="4"
			connect-timeout="1000" max-wait-time="1500" auto-connect-retry="true"
			socket-keep-alive="true" socket-timeout="1500" slave-ok="true"
			write-number="1" write-timeout="0" write-fsync="true" />
	</mongo:mongo>

	<mongo:db-factory dbname="wind" mongo-ref="mongo" />

	<bean id="mongoTemplate" class="org.springframework.data.mongodb.core.MongoTemplate">
		<constructor-arg name="mongoDbFactory" ref="mongoDbFactory" />
	</bean>

	<mongo:repositories base-package="com.wind.repository.mongo" />


</beans>
~~~

## repository
~~~java
package com.wind.repository.mongo;

import org.springframework.data.repository.PagingAndSortingRepository;

import com.wind.entity.mongo.Hello;

public interface HelloRepository  extends PagingAndSortingRepository<Hello, String>{

}
~~~
## entity
~~~java
package com.wind.entity.mongo;

import java.io.Serializable;

import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Document(collection="hello")
public class Hello implements Serializable{
	private static final long serialVersionUID = -2509439493563083804L;

	@Id
	private String id;
	
	private String name;

	public String getId() {
		return id;
	}

	public void setId(String id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return "Hello [id=" + id + ", name=" + name + "]";
	}
}
~~~