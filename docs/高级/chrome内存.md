如何找出具体是哪个变量造成的内存这么大？

## 面板单词释义

### Heap snapshot
堆快照

#### Summary
可以显示按照构造函数名称分组的对象。根据类型了解对象及其内存
#### Comparison
比较多个内存快照在某个操作前后的差异。检查已释放内存的变化和参考计数，确认是否存在内存泄漏及其原因

#### Containment 
通过对象结构视图分析，由顶级对象作为入口

#### Statistic
内存使用饼状

### Allocation instrumentation on timeline
在时间轴（随着时间变化）上分配仪表记录内存信息

### Allocation sampling
内存分配信息采样

待定：https://zhuanlan.zhihu.com/p/80792297
