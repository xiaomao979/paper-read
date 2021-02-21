# 摘要
少样本知识图谱（KG）的补全是当前研究的重点，其中每个任务旨在根据给定的少样本参考实体对（reference entity pairs），来查询关系中未知的事实。最近的尝试通过学习实体和参考的静态表示来解决这个问题，而忽略了它们的动态属性，即，实体可能在任务关系中发挥不同的作用，并且参考可能对查询做出不同的贡献。这项工作提出了自适应注意力网络，通过学习自适应实体和参考表示来实现少样本KG补全。具体而言，实体由自适应邻居编码器建模以识别其面向任务的角色，而参考则由自适应查询感知聚合器建模以区分其贡献。通过注意力机制，实体和参考都可以捕获其细粒度的语义，从而呈现更具表达力的表示形式。在少数情况下，这对于知识获取将更具预测性。对两个公共数据集的链接预测的评估表明，我们的方法以不同的少样本数量获得了最新的最新结果。

# Introduction
KG embedding用来实现KG complement。现有的KG embedding需要大量样本，而且在long-tail relations上表现不好。对于少样本KG补全，之前的方法是借助邻居信息to enhance entity embeddings，邻居权重恒定，这会带来偏差，因为不同语境下权重肯定会变。作者提出了FAAN：Adaptive Attentional Network for Few-Shot KG completion去解决这个问题。

# Background
Few-shot KG Completion：借助少量参考三元组，从candidate entity set中预测尾实体

# Our Approach
1. Adaptive Neighbor Encoder for Entities：利用one-hop邻居，将r视作为h和t的翻译，通过r = t - h获取r的embedding，通过比较r的相似程度来看与邻居的权重关系。
2. Transformer Encoder for Entity Pairs：利用transformer模型，加入位置信息来实现实体对编码。
3. Adaptive Matching Processor：借助参考三元组，利用attention机制，比较相似性得到权重，得到最终预测结果score
