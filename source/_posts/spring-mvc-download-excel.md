title: spring mvc download excel
date: 2015-11-04 12:40:52
tags:
- spring mvc
- js
---
spring mvc下载excel
<!--more-->

$http({
				method : 'post',
				url : url,
				params:params,
				data:data,
				headers: {'Content-Type': 'application/json;charset=UTF-8','X-Requested-With':'XMLHttpRequest'},
				responseType: 'arraybuffer'
			}).success(function(data, status, headers, config) {
				deferred.resolve(data);
				console.log("%c ---------------请求的数据-------------------", 'color:red');
				console.log(data);
				
//				 var blob = new Blob([data], {type: "application/vnd.openxmlformats-officedocument.spreadsheetml.sheet"});
//				 var objectUrl = URL.createObjectURL(blob);
//				 window.open(objectUrl);
				
				 var blob = new Blob([data], {
				        type: 'application/vnd.openxmlformats-officedocument.spreadsheetml.sheet'
				 });
				 saveAs(blob, 'File_Name_With_Some_Unique_Id_Time' + '.xlsx');
				
				$('#foo').hide();
			}).error(function(reason, status, headers, config) {
				deferred.reject(reason);
                $rootScope.alertOption = {content: reason.errors[0].errMsg, show: true};
                $('#foo').hide();
			});