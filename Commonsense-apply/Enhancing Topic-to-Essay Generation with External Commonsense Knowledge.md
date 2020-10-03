# 论文目的
自动 topic-to- essay 生成（TEG）任务是指给定 topic 集合，生成主题相关、段落集的文本。过去的工作仅仅基于给定的主题去执行文本生成，而忽略了大量的常识知识，其实这些常识知识会提供额外的背景知识，这能提高生成文章的新颖性和多样性。为了解决这个问题，本文通过动态记忆机制将外部知识库的知识整合进生成器。除此之外，基于多标签判别器的对抗训练的应用进一步提高了主题一致性。

# 论文方法
## 创建稀疏词向量
- Dictionary Learning-Based Sparse Coding：带正则项的二次型优化问题，利用glove作为初值
- Determining Semantic Atoms Based on Clustering：使用聚类
- Determining Almost Pairwise Orthogonal Semantic Atoms from Actual Word Vectors：从嵌入空间中选择对应于最频繁单词的密集词向量作为第一个包含在D中的向量
## 可解释性方法
- 研究稀疏嵌入矩阵维数可解释性的第一种方法是为每个维数分配人类可解释性特征：

