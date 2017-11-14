现我们有这样的一个需求,在党建缴费中现在缴费的付款方式有两种,一个是支付宝,一个是微信如下图    
![](https://i.imgur.com/ye79XvG.png)     
现在需要在点击支付宝的时候微信百变灰点击微信的时候支付宝变灰,这是我们的需求.在这个需求中其实不算是页面之间的通信而是页面之内的通信.这里使用的方式是通过作用域的方式实现的.主要的实现方式是通过 ng-class = {"green":A,"gray":B},的方式,让点击支付宝的时候选择图标变绿也就是 A 为 true,B=!A,点击微信的时候就是选择支付宝为 !A ,微信为 A=true.而这里的 A B 都是挂在作用域上的数据.
一般这样的通讯是有三个大的解决方案:    
1. 共用服务     
2. 基于事件    
3. 作用域继承
## 共用服务    
共用服务就是注入服务,把需要共享的数据作为一个 service 在需要的 controller 中注入.在 angular 中,服务是一个单例,所以在服务中生成一个对象,该对象就可以利用依赖注入的方式在所有的控制器中实现共享.参看下面的代码     
**service**
 
     angular.module('demo')
    .factory('Data', function(){
        return {
            name: 'htf'
        };
    })
   
**页面**   

	<div ng-controller="childCtrl1">
	  <h3>data in child controller 1 : {{data.name}}</h3>
	  <input class="form-control" type="text" ng-model="data.name">
	</div>
	<div ng-controller="childCtrl2">
	  <h3>data in child controller 2 : {{data.name}}</h3>
	  <input class="form-control" type="text" ng-model="data.name">
	</div>

**控制器**

	.controller('childCtrl1', ['$scope', 'Data', function($scope, Data){
	    $scope.data = Data;
	}])
	
	.controller('childCtrl2', ['$scope', 'Data', function($scope, Data){
	    $scope.data = Data;
	}])
这个方式最为灵活,可以使用在任何需要通信的页面之间.     
## 基于事件    
angularJS 为 $scope 提供了冒泡和隧道机制,$broadcast 会把事件广播给所有的子 Controller,而 $emit 则会将事件冒泡传递给父 Controller,$on 则是 Angular 的事件监听者,利用这三者可以实现上下级和同级(需要构造一个共同得父级 Controller)之间的通讯,并不是很建议这样的通讯方式.     ]
## 作用域继承
每个 Angular 应用都有一个默认的根作用域 $rootscope,根作用域位于最顶层,从他往下挂载着各级作用域,所以可以使用 $rootscope 来作为广播和接受事件,那么就可以实现同级之间的通讯.
**页面**

	<div ng-controller="innerCtrlA">
	    <input class="form-control" type="text" ng-model="name" ng-change="change()">
	</div>
	<div ng-controller="innerCtrlB">
	    <input class="form-control" type="text" ng-model="name" ng-change="change()">
	</div>
**控制器**

	.controller('innerCtrlA', ['$scope', '$rootScope', function($scope, $rootScope){
	    $scope.change = function(){
	        // 广播事件
	        $rootScope.$broadcast('nameChanged', $scope.name);
	    }
	    $rootScope.$on('nameChanged', function(event, data){
	        $scope.name = data;
	    })
	}])
	
	.controller('innerCtrlB', ['$scope', '$rootScope', function($scope, $rootScope){
	    $scope.change = function(){
	        $rootScope.$broadcast('nameChanged', $scope.name);
	    }
	    // 监听事件
	    $rootScope.$on('nameChanged', function(event, data){
	        $scope.name = data;
	    })
	}])