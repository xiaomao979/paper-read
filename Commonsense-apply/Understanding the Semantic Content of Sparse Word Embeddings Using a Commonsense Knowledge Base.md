# 论文目的
1. 探究词向量的可解释性
2. 我们借助常识库提出了一种新的方法来评估单词嵌入的语义内容。
3. 系统地研究了单词嵌入和知识库之间的显式连接。

# 论文方法
## 创建稀疏词向量
- Dictionary Learning-Based Sparse Coding：带正则项的二次型优化问题，利用glove作为初值
- Determining Semantic Atoms Based on Clustering：使用聚类
- Determining Almost Pairwise Orthogonal Semantic Atoms from Actual Word Vectors：从嵌入空间中选择对应于最频繁单词的密集词向量作为第一个包含在D中的向量
## 可解释性方法
- 研究稀疏嵌入矩阵维数可解释性的第一种方法是为每个维数分配人类可解释性特征：

