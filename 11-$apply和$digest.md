## $apply()    
$apply() 会使 NG 进入 $digest cycle,并从 $rootscope 开始遍历(深度优先),检查数据的变更.    
## $digest   
$digest 仅仅会检查该 scope 和 它的子 scope,当你确定当前的操作只是影响他们的时候用 $digest 可以提升一点性能.