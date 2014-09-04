#MapReduce
---

###MapReduce
1. 将分布式计算形式表达成 key/value形式, 计算的输入时key/value数据集合 
2. map过程
	1. 输入的数据集**分成许多数据块**, -- 一个任务分解成多个任务
	2. 为**每个数据块分配一个map任务**,将这些map任务分配到集群的各个节点上,
	3. 每个map任务经过计算会产生一个中间结果(***键值对的数据集合***)
	4. 将这些中间结果键值对**排序**产生一个新的集合
	5. **所有具有相同键值对的被集合在一起**,进入reduce过程
	6. **关键是key,value的选择: 自定义**
3. reduce过程
	1. 将map阶段处理产生的结果进行**规约**,
	2. map和reduce保持高容错性.负载均衡
	3. 示意图<br>![](http://i.imgur.com/pUTroVa.jpg)

###Hadoop与MapReduce
1. 主从结构--一个主节点和多个从节点
	1. 主节点:负责分配任务和调度资源,用户将mapreduce任务交给主节点,主节点再交给从节点
	2. 从节点:负责任务的执行,执行map过程和reduce过程并完成数据迁移