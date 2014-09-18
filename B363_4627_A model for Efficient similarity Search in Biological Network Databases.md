Efficient Similarity Search
===

### 解决问题
- 基于Reference-based indexing methods
- 对于twilight zone里的图的**更快alignment处理**
	
### 创新点
1. 利用mapreduce和hadoop计算similarity, 
2. 定义了fast approximate similarity measures,
3. 不计算similarity而将**某些网络移出twilight zone**的方法.

### 主要步骤
1. 算法模型<br>
![](http://i.imgur.com/1yfRrVo.jpg)
2. twilight zone 处理模型<br>
![](http://i.imgur.com/cNM7rci.jpg)

###核心思想
**Approximate similarity measures** in **aligning the networks**

- Clustering: 2-stage clustering **to reduce the size of twilight zone 用聚类减小每一个的规模**
	1. 第一阶段: 用 **Voltage Clusters(一个图聚类模型)**: 初始用2-4个cluster对图聚类,每一个cluster有8-10个结点
	2. 第二阶段: 减少每个cluster的结点个数到7-8,同时增加少量的cluster以减少处理时间
	3. 把q->d的近似度**近似为**q到d对应的类别(**prototype-由clusters得出的**)的近似度

- Highest Degree Node **to get rid of outlier nodes减小数据库中元素图的规模**
	1. 对于每个网络,试图找到他的**核心子图:尽可能多的表示原图**, 主要找到**highest degree neighbour**
	3. core is more likely to be the most complex subgraph of the network, 还可以离线计算
	4. 随着核心的size大小增加,alignment的准确度增加,时间复杂度也增加了

**shrinking twilight zone** 

1. 改进RINQ的**模糊上界**, Better upper bounds **但是复杂**

2. 用**启发式**的方法,并且利用**生物学里的pathway information** 进行类似**分组**的操作, 有同样的pathway information的图相似可能性更大. 在分组内进行选择reference操作
	- **Heuristic启发式的**:  
		"find" or "discover"启发式的:**根据一定的经验-一定的限制条件**,在问题空间内进行**较少的搜索**.不一定保证问题的解决,能找到较好的结果
		1. 计算qeury q 和网络d的相似度:**用所有点的相似度之和表达(相似度矩阵)**
		2. 计算相似度分数上界:**简单的遍历,相似度矩阵的最大值**
	- **Heuristic criteria**: 启发式的判断准则
		1. q和d的**biological pathways 相同**,而且相似度尽可能大
		2. **或者**相似度的一半大于限定值(cut-off value)

###问题
1. table1和图3,4
2. **pathway information**
3. BLAST:
	BLAST for Basic Local Alignment Search Tool is an algorithm for comparing primary biological sequence information, such as the amino-acid sequences of different 
