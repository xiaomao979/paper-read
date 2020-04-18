# 论文目的
给定三元组判断是否这个三元组是否为合理的常识（We develop neural network models for scoring tuples on arbitrary phrases and evaluate them by
their ability to distinguish true held-out tuples from false ones）

# 论文方法
## Bilinear Models
将实体和关系分别embedding，得到实体向量和关系矩阵，其中实体向量是通过预训练好的词向量（通过skip-gram）embedding，而关系向量是通过随机初始化得到的。
score = u_{1}^{T}M_{R}u_{2}

## loss function
使用自定义的Hinge Loss和Binary Cross Entropy

## Negative Examples
通过三种方法得到Negative Examples：1.互换subject，2.互换object，3.互换关系

# 实验方法
## 数据集获取
The tuples are obtained from the Open Mind Common Sense (OMCS) entries in the ConceptNet5 dataset

## Word Embeddings
使用跳字模型预训练embedding
