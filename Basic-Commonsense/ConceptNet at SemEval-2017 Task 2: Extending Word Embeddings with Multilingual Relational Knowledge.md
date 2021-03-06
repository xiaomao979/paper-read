# 论文目的
利用常识库来解决 多语言和跨语言语义词相似性（Multilingual and Cross-lingual Semantic Word Similarity） 的问题  
子任务1比较五种语言中每一种语言中的一对单词    
子任务2比较十对不同语言中每一种语言中的一对单词。  
# 论文方法
1. 翻新Retrofitting（Faruqui et al.2015）是使用知识图谱（嵌入）调整现有词嵌入矩阵的过程。本文构建词向量的方法即为Retrofitting
2. 使用多个源的词向量并对齐处理
3. 为了减少空间复杂度，我们对通过词频对词表进行过滤，选择出现频率较多的词汇组成最终的词汇表
4. 将原词汇表中每个词向量的维度降维 并 删除来自连接多个嵌入源的冗余，降维使用SVD分解（类似于PCA降维）
5. 对于不在词汇表中的单词，作者之前的做法是在常识图中找邻居，利用邻居词向量的均值作为该词汇的词向量，若该词汇没有邻居，则仍为OOV（out-of-vocabulary）。本次任务中，作者针对仍为OOV的词汇进行两种策略处理：如果一个术语与矩阵M3中的向量不相关，则我们首先在英语中查找相同拼写的术语的向量。如果存在该向量，则使用它；当找不到以其给定语言或英语提供的术语时，
我们在词汇表中寻找以给定术语为前缀的术语。如果没有找到，则从未知术语的末尾丢弃一个字母，然后寻找它作为前缀，如果还是找不到，就继续删除字母，直到找到结果为止。当前缀产生结果时，我们将所有结果向量的均值用作单词的向量。
