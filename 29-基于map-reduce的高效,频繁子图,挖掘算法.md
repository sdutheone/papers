29-基于map-reduce的高效,频繁子图,挖掘算法
===


摘要
---
在扩展边生成新的子图时，使用已经**挖掘出的支持度为 k-1 的频繁子图**生成**频繁度为 k 的频繁子图**。同时，检查是否存在待扩展生成的子图.

##论文思想:



### 流程图
![](http://i.imgur.com/sbrxaFc.jpg)
### 主要步骤
1. ParserMapper:相当于初始化用户输入. **输出**为<key=边信息,value=其他>
2. MapperB:**按照边来划分**. **输出为**<key=边信息(格式化),value=标识+图ID)>
3. ReducerB:按相同的边,**计算support**,**输出为**<key=指定格式的边,value=空>
4. MapperA: **按照图ID划分**. **输出为**<key=边信息(按图ID划分),value=空>
5. ReducerA: **从k-1维扩展到k维**: **输出为**<key=指定格式边,value=空>
6. MapperB...循环

>MapperB/ReducerB: 子图的分类
>MapperA/ReducerA: 扩展边

### **ReducerA**:基于边的候选产生--去除重复性

- 加入潜在的候选边<br>
- 将ReducerB挖掘出的图解析成单独的边(映射关系)<br>
- 扩展边时判断(**避免产生复制图--相同的图**)
	- 利用集合排序的思想去避免重复
	- 两个集合A,B. B对应**当前最大频繁子图**,A是临时集合

**算法通用性?**

- 用排序保证
- 先部分排序:重点按照字母表排序
- 后整体排序:起点排序
```
| Left-Aligned  | Center Aligned  | Right Aligned |
| :------------ |:---------------:| -----:|
| col 3 is      | some wordy text | $1600 |
| col 2 is      | centered        |   $12 |
| zebra stripes | are neat        |    $1 |
```
- [x] @mentions, #refs, [links](), **formatting**, and <del>tags</del> supported
- [x] list syntax required (any unordered or ordered list supported)
- [x] this is a complete item
- [ ] this is an incomplete item
