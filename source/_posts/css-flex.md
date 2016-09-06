title: css flex
date: 2016-08-23 14:58:29
tags:
- css
---
css flex 弹性盒子模型
<!--more-->

任何一个容器都可以设置为flex布局
~~~css
.box{
  display: flex;
}
~~~


容器的属性

- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content


flex-direction: row|row-reverse|column|column-reverse|initial|inherit;




属性值
	
| 值		  				| 描述		    									|
| ------- 				|:-----------									   :|
| row		  			| 默认值。灵活的项目将水平显示，正如一个行一样	   		| 
| row-reverse		  	| 与 row 相同，但是以相反的顺序		    			| 
| column		  		| 灵活的项目将垂直显示，正如一个列一样	    			| 
| column-reverse		  	|与 column 相同，但是以相反的顺序	    				|
| initial		  		| 设置该属性为它的默认值		    					|
| inherit		 		| 从父元素继承该属性		    						|







# REF

http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool

