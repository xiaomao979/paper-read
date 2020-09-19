# 论文目的
实现常识问答——常识问答要用到外部知识，现有的常识问答方法有两种：they either generate evidence from human-annotated evidence or extract evidence from a homogeneous knowledge source like structured knowledge ConceptNet

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

# 论文亮点
1. 实验做得极其充分
