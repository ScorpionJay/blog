title: responsive-layout
date: 2015-11-10 15:29:12
tags:
- js
- html
---
响应适
<!--more-->
~~~html
<!DOCTYPE html>
<html>
	<head>
	<meta chartset="utf-8">
		<title>响应</title>
		<meta name="viewport" content="width = device-width,initial-scale=1,user-scalable=yes">
		<style type="text/css">

			body {
			    font-size: 20px;
			    color:blue;
			    background-color: red;
			}

			@media (min-width: 768px) and (max-width: 1000px){
			  body {
			    font-size: 40px;
			    color:black;
			    background-color: blue;
			  }
			}

			@media (min-width:1000px) and (max-width: 1024px){
			  body {
			    font-size: 60px;
			    color:red;
			    background-color: yellow;
			  }
			}

			@media (min-width:1024px) and (max-width:1366px){
			  body {
			    font-size: 80px;
			    color:yellow;
			    background-color: black;
			  }
			}

			@media(min-width:1366px){
			  body {
			    font-size: 200px;
			    color:rgba(00,55,66,0.5);
				background-color: rgba(100,55,66,0.5);			 
			 }
			}
			
		</style>
	</head>
	<body>
		响应
	</body>
</html>
~~~
