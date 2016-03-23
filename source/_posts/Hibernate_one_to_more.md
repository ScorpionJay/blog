title: Hibernate一对多
date: 2015-09-08 14:36:30
tags:
- hibernate
---

Hibernate one to more
<!--more-->
一对多
班级 学生

~~~xml
		<!-- 一对多 -->
		<set name="students" table="student">
			<key column="gid" />
			<one-to-many class="com.hibernate.entity.Student" />
		</set>
~~~