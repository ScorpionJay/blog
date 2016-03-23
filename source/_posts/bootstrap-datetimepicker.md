title: bootstrap-datetimepicker
date: 2015-10-22 23:41:06
tags:
- bootstrap
- js
---
时间选择插件
<!--more-->

	<!DOCTYPE html>
	<html>
	<head>
	    <title>datetimepicker</title>
	    <meta charset="UTF-8">
	    <link href="http://apps.bdimg.com/libs/bootstrap/3.3.4/css/bootstrap.min.css" rel="stylesheet" media="screen">
	    <link href="css/bootstrap-datetimepicker.min.css" rel="stylesheet" media="screen">
	</style>
	</head>
	
	<body>
	    <div>
	        <lable class="col-md-2 control-label">year</lable>
	        <input  id="y" readonly /> 
	    </div>
	
	    <div>
	        <lable class="col-md-2 control-label">year month</lable>
	        <input  id="ym" readonly /> 
	    </div>
	     
	    <div>
	        <lable class="col-md-2 control-label">year month day</lable>
	        <input  id="ymd" readonly /> 
	    </div>
	</body>
	<script type="text/javascript" src="http://apps.bdimg.com/libs/jquery/2.1.4/jquery.min.js"></script>
	<script type="text/javascript" src="http://apps.bdimg.com/libs/bootstrap/3.3.4/js/bootstrap.min.js"></script>
	<script type="text/javascript" src="js/bootstrap-datetimepicker.js" charset="UTF-8"></script>
	<script>
	    $('#y').datetimepicker({
	        format: "yyyy",
	        autoclose:true,
	        startView: "decade",
	        minView: "decade",
	        language: "zh-CN",
	    });
	    $('#ym').datetimepicker({
	       format: "yyyy-mm",
	        autoclose:true,
	        startView: "year",
	        minView: "year",
	        language: "zh-CN",
	    });
	    $('#ymd').datetimepicker({
	        format: "yyyy-mm-dd",
	        language:  'zh-CN',
	        autoclose:true,
	        todayHighlight: true,
	        startView: "month",
	        minView: "month",
	        forceParse: 0
	    });
	</script>
	</html>
