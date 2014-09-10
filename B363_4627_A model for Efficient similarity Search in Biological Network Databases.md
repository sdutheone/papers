Efficient Similarity Search
===

##Background
Query Network, 生物网络

###Reference-based indexing methods
**Alinement?**
- use a reference network set R to represent the biological database D -- created by the D. **R not too big and only contains small sized networks**.
- transform the query to Database (q-D) which is time-consuming to q-R and R-D **alignment**
- 利用相似度的上确界和下确界来简化similarity的计算. 当similarity 处于中间水平(twilight zone)时,需要计算(计算复杂度决定了算法的复杂度) 
- 算法性能取决于
	1. 计算similarity的复杂度
	2. twilight zone的大小 -- RINQ方法和QNET
	
###创新点
	1. 利用mapreduce和hadoop计算similarity, 
	2. 定义了fast approximate similarity measures,
	3. 不计算similarity而将**某些网络移出twilight zone**的方法.

###算法模型
1. 算法模型<br>
![](http://i.imgur.com/1yfRrVo.jpg)
2. twilight zone 处理模型<br>
![](http://i.imgur.com/cNM7rci.jpg)

###Approximate similarity measures
1. Clustering: 2-stage clustering
	1.  first use Voltage Clusters: 为每个图分配2-4个cluster,每一个cluster有8-10个结点
	2.  第二阶段: 减少每个cluster的结点个数,同时增加少量的cluster以减少处理时间
	3. 把q->d的查询**近似为**q到d对应的clusters的查询

2. Highest Degree Node
	1. 缩小数据库中元素的规模: 对于每个网络,试图找到他的**核心子图**
	2. 主要找到highest degree neighbour
	3. core is more likely to be the most complex subgraph of the network
	4. 随着核心的size大小增加,alignment的准确度增加,时间复杂度也增加了

###shrinking twilight zone
1. Better upper bounds 
	但是复杂
2. 用自适应的方法,利用生物学里的pathway information 进行类似**分组**的操作, 有同样的pathway information的图相似可能性更大. 在分组内进行选择reference操作
3. Heuristic:  "find" or "discover"启发式的:根据一定的经验-一定的限制条件,在问题空间内进行**较少的搜索**.不一定保证问题的解决,能找到较好的结果
	1. 计算qeury q 和网络d的相似度:用所有点的相似度之和表达(相似度矩阵)
	2. 计算相似度分数上界:相似度矩阵的最大值
4. criteria: 准则
	1. q和d的biological pathways 相同,而且相似度最大
	2. **或者**相似度的一半大于限定值(cut-off value)


###问题
1. alignment: 比对
2. query network:
	query也是一个图,要查询与这个图相似的图
3. table1和图3,4
4. pathway information
5. BLAST:BLAST for Basic Local Alignment Search Tool is an algorithm for comparing primary biological sequence information, such as the amino-acid sequences of different 
6. recall rate