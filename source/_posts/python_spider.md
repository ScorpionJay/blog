title: python spider
date: 2016-10-25 18:06:31
tags:
- python
---
python spider
<!--more-->
~~~python
import urllib2
import re
import os

log = open('log.txt','w')
log.write('****************get pic*************\n\n')  

page = 1
index = 0
while page <= 10:
	data = urllib2.urlopen('http://www.ssyer.com/index_page_'+ str(page) +'.html').read()
	log.write('**********************'+str(page)+'\n\n')
	reg = r'<img class="pic" src="(.*?)"  />'
	lists = re.findall(reg,data)
	for item in lists:
		print str(item)
		image = urllib2.urlopen('http://www.ssyer.com/'+item).read()
		file = open( str(index) + '.jpg','wb')
		file.write(image)
		file.flush
		index+=1

	page+=1
~~~
