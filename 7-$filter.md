## $filter 简述   
1. [**$filter**](http://docs.ngnice.com/api/ng/filter/filter) 是用来数据格式化的专用服务   
2. AngularJS 内置了 9 个 [**$filter**](http://docs.ngnice.com/api/ng/filter/filter):currency,data,filter,JSON,limitTo,lowercase,number,orderBy,uppercase   
3. [**$filter**](http://docs.ngnice.com/api/ng/filter/filter) 可以嵌套使用(用管道符号|分隔)
4. [**$filter**](http://docs.ngnice.com/api/ng/filter/filter) 是可以传递参数的
5. 用户可以自定义自己的 [**$filter**](http://docs.ngnice.com/api/ng/filter/filter)    

currency 货币 
data 日期   
JSON Allows you to convert a JavaScript object into JSON string.   
orderBy 排序  
number 数字  
limitTo : Creates a new array or string containing only a specified number of elements. The elements are taken from either the beginning or the end of the source array or string, as specified by the value and sign (positive or negative) of limit (创建一个仅包含指定数量元素的新数组或字符串。元素取自源数组或字符串的开始或结尾，如限值的值和符号（正或负）所指定）)    
filter : Selects a subset of items from array and returns it as a new array(从数组中选择一个子集，并将其作为新数组返回)   
