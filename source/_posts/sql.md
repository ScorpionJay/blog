title: sql
date: 2015-08-20 15:48:11
tags:
- sql
---

sql学习
<!--more-->

	--创建表
	create table t1(
	id1 int,
	name1 varchar(10)
	);
	create table t2(
	id2 int,
	name2 varchar(10)
	);
	create table t3(
	id2 int,
	name2 varchar(10)
	);

	--插入数据
	INSERT into t1(id1,name1) values(1,"jay1");
	INSERT into t1(id1,name1) values(2,"jay2");
	INSERT into t1(id1,name1) values(3,"jay3");
	INSERT into t1(id1,name1) values(4,"jay4");
	INSERT into t1(id1,name1) values(5,"jay4");
	
	INSERT into t2(id2,name2) values(1,"jay11");
	INSERT into t2(id2,name2) values(2,"jay22");
	INSERT into t2(id2,name2) values(3,"jay33");
	INSERT into t2(id2,name2) values(6,"jay66");
	
	INSERT into t3(id2,name2) values(1,"jay111");
	INSERT into t3(id2,name2) values(2,"jay222");
	INSERT into t3(id2,name2) values(3,"jay333");
	INSERT into t3(id2,name2) values(6,"jay666");
	INSERT into t3(id2,name2) values(7,"jay777");

	--查询
	select * from t1;
	select * from t2;
	
	select * from t1,t2 where t1.id1 = t2.id2;
	
	--左连接
	select * from t1 left join t2 on t1.id1 = t2.id2;
	--右连接
	select * from t2 left join t1 on t1.id1 = t2.id2;
	
	--内连接
	select * from t1 inner join t2 on t1.id1 = t2.id2;
	
	-- 分组
	select count(*) as 数量, name1, id1 from t1 group by name1;
	
	select * from t3 left join t2 on t3.id2 = t2.id2 left join t1 on t1.id1=t3.id2;
	
	--更新
	update t1 set id1=id1-100

	--相关子查询 子查询语句依赖父语句
     select *，
            (select 
				sum(amount) from income where id = draw.ID
			 and  DATE_SUB(CURDATE(), INTERVAL 7 DAY) <= income_time) as money
	 from 
			withdraw as draw ,
            dietican as d,
            bankcard as card
 	 where 
        draw.DIETICAN_ID = d.DIETICAN_ID 
     and 
		draw.BANKCARD_ID = card.BANKCARD_ID
