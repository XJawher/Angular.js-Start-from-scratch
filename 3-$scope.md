## $scope 
**$scope** 是一个 POJO(Plain Old JavaScript Object) 是一个 js 对象   
**$scope** 提供了一些工具的方法, $watch()/$apply()    
**$scope** 是表达式的执行环境,或者叫作用域    
**$scope** 是一个树形结构,和 DOM 标签是平行的.    
**$scope** 子对象是可以继承父对象的 **$scope** 的属性和方法  
**$scope** 有一个根 **$scope** 一般都是在 ng-app 上.   
**$scope** 可以传播事件,类似 DOM 事件,可以向上也可以向下   
**$scope** 是整个 angular 的基础,不仅仅是 MVC 和 实现双向数据绑定的基础,是非常重要的一个内容  
**$scope** 他有非常多的封装,    
**$scope** 调试,可以用 angular.element($0).scope() 来调试当前元素的 scope 的内容    
## $scope 生命周期 
**Creation>Watcher registration>Model mutation>Mutation observation>Scope destruction**首先是创建,然后是注册监控,接着是检测模型的变化,然后观察模型有没有脏(脏是啥意思?被污染??还是不用了??)最后被销毁