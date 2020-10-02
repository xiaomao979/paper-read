# 论文目的
实现带attention机制的BERT对常识推断任务的可执行性

# 论文方法
## 创建稀疏词向量
- Dictionary Learning-Based Sparse Coding：带正则项的二次型优化问题，利用glove作为初值
- Determining Semantic Atoms Based on Clustering：使用聚类
- Determining Almost Pairwise Orthogonal Semantic Atoms from Actual Word Vectors：从嵌入空间中选择对应于最频繁单词的密集词向量作为第一个包含在D中的向量
## 可解释性方法
- 研究稀疏嵌入矩阵维数可解释性的第一种方法是为每个维数分配人类可解释性特征：

# 实验方法
## dataset
- English Reddit dataset
- Chinese Weibo dataset

## 实验内容
1. 在数据集上对比baseline效果
2. Ablation Study——对比模型简化版本以证明每个模块的有效性
3. case study
4. 误差分析——the lack of evidence, similar evidence and dataset noise


# 论文亮点
实验部分采用多重语言
