Efficient Similarity Search
===

##Background
Query Network, 生物网络

###Reference-based indexing methods
- use a reference network set R to represent the biological database D -- created by the D. **R not too big and only contains small sized networks**.
- transform the query to Database (q-D) which is time-consuming to q-R and R-D **alignment**
- 利用相似度的上确界和下确界来简化similarity的计算. 当similarity 处于中间水平(twilight zone)时,需要计算(计算复杂度决定了算法的复杂度) 
- 算法性能取决于
	1. 计算similarity的复杂度
	2. twilight zone的大小 -- RINQ方法和QNET
	
###创新点
	1. 利用mapreduce和hadoop计算similarity, 定义了fast approximate similarity measures
	2. 不计算similarity而将**某些网络移出weilight zone**的方法.

