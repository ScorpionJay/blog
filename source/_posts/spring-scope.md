---
title: spring-scope
date: 2015-06-30 23:59:19
tags:
- spring
---
spring scope
<!--more-->
spring bean 作用域

单例（默认） 原型
@Scope("singleton")
@Scope("prototype")

注意
这里的原型是获取的时候会new一个实例

在类中@autowired 那么这个类里就是同一个，不会再去new

在另外一个类中调用才会去new

所以在controller中

@Autowired
private ResultVo resultVo;

每个方法中返回都是同一个，解决方法只能都赋值，或者写一个清空的方法调用。

不知道这么做是否可以。

尽量的少原型，一万个请求就实例一万个类。