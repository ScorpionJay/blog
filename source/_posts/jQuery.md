title: jQuery
date: 2015-08-28 10:40:27
tags:
- jQuery
---

jQuery 是一个 JavaScript 库。
jQuery 极大地简化了 JavaScript 编程。
<!--more-->

1.ready
源码
````javascript
jQuery.fn.ready = function( fn ) {
	// Add the callback
	jQuery.ready.promise().done( fn );

	return this;
};
jQuery.extend({
	// Is the DOM ready to be used? Set to true once it occurs.
	isReady: false,

	// A counter to track how many items to wait for before
	// the ready event fires. See #6781
	readyWait: 1,

	// Hold (or release) the ready event
	holdReady: function( hold ) {
		if ( hold ) {
			jQuery.readyWait++;
		} else {
			jQuery.ready( true );
		}
	},

	// Handle when the DOM is ready
	ready: function( wait ) {

		// Abort if there are pending holds or we're already ready
		if ( wait === true ? --jQuery.readyWait : jQuery.isReady ) {
			return;
		}

		// Make sure body exists, at least, in case IE gets a little overzealous (ticket #5443).
		if ( !document.body ) {
			return setTimeout( jQuery.ready );
		}

		// Remember that the DOM is ready
		jQuery.isReady = true;

		// If a normal DOM Ready event fired, decrement, and wait if need be
		if ( wait !== true && --jQuery.readyWait > 0 ) {
			return;
		}

		// If there are functions bound, to execute
		readyList.resolveWith( document, [ jQuery ] );

		// Trigger any bound ready events
		if ( jQuery.fn.triggerHandler ) {
			jQuery( document ).triggerHandler( "ready" );
			jQuery( document ).off( "ready" );
		}
	}
});
~~~
JavaScript window.onload 事件和 jQuery ready 函数有何不同？
1.要等待 DOM 被创建还要等到包括大型图片、音频、视频在内的所有外部资源都完全加载。如果加载图片和媒体内容花费了大量时间，用户就会感受到定义在 window.onload 事件上的代码在执行时有明显的延迟。
2.多次使用，onloay会覆盖，ready只会按照顺序调用


2.添加文本
after before appendTo

3.你如何利用jQuery来向一个元素中添加和移除CSS类? (答案)

通过利用 addClass() 和 removeClass() 这两个 jQuery 方法。动态的改变元素的class属性可以很简单例如. 使用类“.active"来标记它们的未激活和激活状态，等等.


4.问题：jQuery中有哪几种类型的选择器？

回答：从我自己的角度来讲，可以有3种类型的选择器，如下：

1、基本选择器：直接根据id、css类名、元素名返回匹配的dom元素。

2、层次选择器：也叫做路径选择器，可以根据路径层次来选择相应的DOM元素。

3、过滤选择器：在前面的基础上过滤相关条件，得到匹配的dom元素。

5.如何检查某个元素是否存在

if ($('#someDiv').length) { //万岁！！！它存在……  } 