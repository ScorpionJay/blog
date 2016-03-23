title: spring quartz
date: 2015-10-29 23:47:48
tags: 
- java
- spring
---
quartz
<!--more-->
## java
~~~java
package com.wind.scheduler;

import org.quartz.JobExecutionContext;
import org.quartz.JobExecutionException;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.scheduling.quartz.QuartzJobBean;
import org.springframework.stereotype.Component;

@Component
public class QuartzTest  extends QuartzJobBean{

	//@Autowired
	//IHelloService helloService;

	private static final Logger logger = LoggerFactory.getLogger(QuartzTest.class);
	
	@Override
	protected void executeInternal(JobExecutionContext arg0) throws JobExecutionException {
		//String str = helloService.test();
		logger.info("继承QuartzJobBean的方式-调度"  + "进行中..." );
		//System.out.println("继承QuartzJobBean的方式-调度"  + "进行中..." );
	}

}

~~~


## xml
~~~xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:context="http://www.springframework.org/schema/context"
	xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
             http://www.springframework.org/schema/context
             http://www.springframework.org/schema/context/spring-context.xsd
             http://www.springframework.org/schema/tx  
    		 http://www.springframework.org/schema/tx/spring-tx.xsd ">


	<context:component-scan base-package="com.wind.scheduler" >
		<context:include-filter type="annotation" expression="org.springframework.stereotype.Component"/>
		<context:exclude-filter type="annotation" expression="org.springframework.stereotype.Service"/>
	</context:component-scan>
	
	<bean name="job1"
		class="org.springframework.scheduling.quartz.JobDetailFactoryBean">
		<property name="jobClass" value="com.wind.scheduler.QuartzTest" />
		<property name="durability" value="true" />
		<property name="requestsRecovery" value="true" />
	</bean>

	<!-- 对应于作业继QuartzJobBean类的方式 -->
	<!-- 没两分钟调用一次 0 0/2 * * * ? * -->
	<bean id="cronTrigger"
		class="org.springframework.scheduling.quartz.CronTriggerFactoryBean">
		<property name="jobDetail" ref="job1" />
		<property name="cronExpression" value="0 0/1 * * * ? *" />
	</bean>

	<bean class="org.springframework.scheduling.quartz.SchedulerFactoryBean">
		<property name="triggers">
			<list>
				<ref bean="cronTrigger" />
			</list>
		</property>
	</bean>

</beans>
~~~
