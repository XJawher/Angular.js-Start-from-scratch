## service 和 Provider    
当我们发现在不同的 Controller 中有相同的代码的时候,就需要我们把这些代码抽成一个服务,让他公用下面有一些 service 服务   
1. $http 服务    
2. 创建自己的 service    
3. Service 特性     
4. Service Factory Provider 的区别   
5. 使用 $filter 服务    
6. 其他内置的 Service 介绍    
### $http

	$http({
	    method: 'GET',
	    url: 'psw.json'
	  }).then(function successCallback(response) {
	      console.log(response.data.login[0])
	      var JsonCell = parseInt(response.data.login[0].username);
	      var JsonPsw = parseInt(response.data.login[0].password);
	
	      if (cellphone === JsonCell || psw === JsonPsw) {
	        avicitMobileApi.createTemplate('identity', 'modules/identity/identity.html', $scope);
	      }else {
	      var alertPopup = $ionicPopup.alert({
	       title: '错误!!!',
	       template: '手机号或者密码不正确!!'
	      });
	    }
	  })
### service 
编写自己的服务      
**Service** 的特性    
1. Service 都是单例的     
2. Service 由 $injector 负责实例化    
3. Service 在整个应用的生命周期中存在,可以用来共享数据     
4. 在需要使用的地方利用依赖注入机制注入 service   
5. 自定义的 Service 要放在内置的 Service 后面   
6. 内置的 Service 是以 $ 符号开头的,自定义的 Service 应该避免   

	var myServiceApp = angular.module("myServiceApp",[]);
	myServiceApp.factory("userListService",["$http",
	    function ($http) {
	      var doRequest = function (username,path) {
	        return $http ({
	          method:'get',
	          url:'users.json'
	        });
	      }
	      return {
	        userList : function (username) {
	          return doRequest(username,'userList')
	        }
	      }
	    }
	  ])
	
	myServiceApp.controller('serviceController',['$scope','$timeout','userListService',
	  function ($scope,$timeout,userListService) {
	    var timeout;
	    $scope.$watch('username',function (newuserName) {
	      if (newuserName) {
	        if (timeout) {
	          $timeout.cancel(timeout)
	        }
	        timeout = $timeout(function() {
	          userListService.userList(newuserName)
	            .success(function(data,status) {
	              $scope.users = data;
	            })
	        },350)
	      }
	    })
	  }])























  
