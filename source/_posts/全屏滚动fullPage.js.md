title: 全屏滚动fullPage.js
date: 2015-09-21 14:08:31
tags:
- js
---

“全屏”效果
<!--more-->


[githu bfullPage.js源码](https://github.com/alvarotrigo/fullPage.js "fullPage")

![](/img/fullPage.png)

##安装

	// With npm
	npm install fullpage.js

##引入
依赖jquery
	
	<!--fullPage css-->
	<link rel="stylesheet" type="text/css" href="jquery.fullPage.css" />
	
	<!--jquery 使用百度的cdn-->
	<script src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.js"></script>
	
	<!-- This following line is optional. Only necessary if you use the option css3:false and you want to use other easing effects rather than "linear", "swing" or "easeInOutCubic". -->
	<script src="http://apps.bdimg.com/libs/jqueryui/1.9.2/jquery-ui.min.js"></script>
	
	<!-- This following line is only necessary in the case of using the plugin option `scrollOverflow:true` -->
	<script type="text/javascript" src="vendors/jquery.slimscroll.min.js"></script>
	
	<!--fullPage js-->
	<script type="text/javascript" src="jquery.fullPage.js"></script>

##Html结构

~~~html
<div id="fullpage">
    <div class="section">Some section</div>
    <div class="section">Some section</div>
    <div class="section">Some section</div>
    <div class="section">Some section</div>
</div>
~~~

##初始化

简单的初始化
~~~js
$(function(){
	 $('#fullpage').fullpage();
});
~~~

复杂的初始化
~~~js
$(function() {
    $('#fullpage').fullpage({
        //Navigation
        menu: false,
        lockAnchors: false,
        anchors:['firstPage', 'secondPage'],
        navigation: false,
        navigationPosition: 'right',
        navigationTooltips: ['firstSlide', 'secondSlide'],
        showActiveTooltip: false,
        slidesNavigation: true,
        slidesNavPosition: 'bottom',

        //Scrolling
        css3: true,
        scrollingSpeed: 700,
        autoScrolling: true,
        fitToSection: true,
        fitToSectionDelay: 1000,
        scrollBar: false,
        easing: 'easeInOutCubic',
        easingcss3: 'ease',
        loopBottom: false,
        loopTop: false,
        loopHorizontal: true,
        continuousVertical: false,
        normalScrollElements: '#element1, .element2',
        scrollOverflow: false,
        touchSensitivity: 15,
        normalScrollElementTouchThreshold: 5,

        //Accessibility
        keyboardScrolling: true,
        animateAnchor: true,
        recordHistory: true,

        //Design
        controlArrows: true,
        verticalCentered: true,
        resize : false,
        sectionsColor : ['#ccc', '#fff'],
        paddingTop: '3em',
        paddingBottom: '10px',
        fixedElements: '#header, .footer',
        responsiveWidth: 0,
        responsiveHeight: 0,

        //Custom selectors
        sectionSelector: '.section',
        slideSelector: '.slide',

        //events
        onLeave: function(index, nextIndex, direction){},
        afterLoad: function(anchorLink, index){},
        afterRender: function(){},
        afterResize: function(){},
        afterSlideLoad: function(anchorLink, index, slideAnchor, slideIndex){},
        onSlideLeave: function(anchorLink, index, slideIndex, direction, nextSlideIndex){}
    });
});
~~~
