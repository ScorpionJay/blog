title: 	Bootstrap Grid System
date: 2015-11-18 14:19:25
tags:
- html
- bootstrap
- css
---

<link rel="stylesheet" href="//cdn.bootcss.com/bootstrap/3.3.5/css/bootstrap.min.css">
栅格系统
<!--more-->
<div class="container">
<h1>Bootstrap Grid System</h1><div class="container"><h2 class="page-header">col-xs</h2>
<div class="row"><div class="col-xs-4 btn-success" >col-xs-4</div><div class="col-xs-4 btn-warning">col-xs-4</div><div class="col-xs-4 btn-info">col-xs-4</div>
</div>
<h2 class="page-header">col-sm</h2>
<div class="row"><div class="col-sm-4 btn-success">col-xs-4</div><div class="col-sm-4 btn-warning">col-xs-4</div><div class="col-sm-4 btn-info">col-xs-4</div>
</div>
<h2 class="page-header">col-md</h2>
<div class="row"><div class="col-md-4 btn-success">col-xs-4</div><div class="col-md-4 btn-warning">col-xs-4</div><div class="col-md-4 btn-info">col-xs-4</div>
</div>
<h2 class="page-header">col-lg</h2>
<div class="row"><div class="col-lg-4 btn-success">col-xs-4</div><div class="col-lg-4 btn-warning">col-xs-4</div><div class="col-lg-4 btn-info">col-xs-4</div>
</div>

<h2 class="page-header">Respond</h2>
<div class="row"><div class="col-xs-6 col-lg-3 btn-success">col-xs-3</div><div class="col-xs-6 col-lg-3 btn-warning">col-xs-3</div><div class="col-xs-6 col-lg-3 btn-info">col-xs-3</div><div class="col-xs-6 col-lg-3 btn-primary">col-xs-3</div>
</div>
</div>
</div>


~~~html
<!DOCTYPE html>
<html lang="zh-CN">
	<head>
		<meta charset="utf-8">
		<meta name="viewport" content="width=device-width,initial-scale=1">
		<title>mars</title>
		<link rel="stylesheet" type="text/css" href="assets/bootstrap/stylesheets/bootstrap.css">
	</head>
	<body>
		<div class="container-fluid">
			<h1>Bootstrap Grid System</h1>
			<div class="container">
				<h2 class="page-header">col-xs</h2>
				<div class="row">
					<div class="col-xs-4 btn-success" >col-xs-4 col-xs-4</div>
					<div class="col-xs-4 btn-warning">col-xs-4</div>
					<div class="col-xs-4 btn-info">col-xs-4</div>
				</div>
				<h2 class="page-header">col-sm</h2>
				<div class="row">
					<div class="col-sm-4 btn-success">col-xs-4</div>
					<div class="col-sm-4 btn-warning">col-xs-4</div>
					<div class="col-sm-4 btn-info">col-xs-4</div>
				</div>
				<h2 class="page-header">col-md</h2>
				<div class="row">
					<div class="col-md-4 btn-success">col-xs-4</div>
					<div class="col-md-4 btn-warning">col-xs-4</div>
					<div class="col-md-4 btn-info">col-xs-4</div>
				</div>
				<h2 class="page-header">col-lg</h2>
				<div class="row">
					<div class="col-lg-4 btn-success">col-xs-4</div>
					<div class="col-lg-4 btn-warning">col-xs-4</div>
					<div class="col-lg-4 btn-info">col-xs-4</div>
				</div>
				<h2 class="page-header">Respond</h2>
				<div class="row">
					<div class="col-xs-6 col-lg-3 btn-success">col-xs-3</div>
					<div class="col-xs-6 col-lg-3 btn-warning">col-xs-3</div>
					<div class="col-xs-6 col-lg-3 btn-info">col-xs-3</div>
					<div class="col-xs-6 col-lg-3 btn-primary">col-xs-3</div>
				</div>
				<h2 class="page-header">xxx</h2>
				<div class="row">
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
					<div class="col-md-1" style="border:1px red solid">col-md-1</div>
				</div>
				xs
				<div class="row">
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
					<div class="col-xs-1" style="border:1px red solid">col-md-1</div>
				</div>

				<h2 class="page-header">offset</h2>
				<div class="row">
					<div class="col-xs-4 btn-warning ">col-xs-4</div>
					<div class="col-xs-4 btn-primary col-xs-offset-4">col-xs-4</div>
				</div>

				<h2 class="page-header">pull push</h2>
				<div class="row">
					<div class="col-md-8  col-md-push-4 btn-warning">col-xs-4</div>
					<div class="col-md-4 col-md-pull-8  btn-primary">col-xs-4</div>
				</div>
				
			</div>
		</div><!---container-->
	</body>
</html>

~~~
