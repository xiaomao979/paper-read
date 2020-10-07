# 论文目的
传统的常识获取需要昂贵的人力标注，而且规模较小。本文提出在linguistic graphs上挖掘常识知识，从而构建大规模常识图谱
# 论文方法
## 任务描述
我们首先定义从语言图挖掘常识知识的任务。 给定种子常识知识集C（包含m个元组）和语言图集G（包含n个语言图G），其中m << n。 每个常识事实都采用元组格式（h，r，t）属于 C，其中r 属于 R，这是人类定义的常识关系的集合（例如，“ UsedFor”，“ CapableOf”，“ AtLocation”，“ MotivatedByGoal”） ，h和t是任意短语。 我们的目标是在C的帮助下从G推断出一个新的常识知识集C +（具有m +条常识知识），使得m + >> m
## Method
首先，对于每个种子常识元组（h，r，t）∈C，我们匹配并选择包含h和t中所有项的支持语言图，然后为每个常识关系提取匹配的常识的语言模式 元组和语言图对。 接下来，我们使用模式过滤模块来选择质量最高的模式。 最后，我们训练一个判别模型来评估所提取常识知识的质量。
- Knowledge Resources ：常识知识图谱使用conceptnet，linguistic knowledge resource使用ASER
- Pattern Extraction ：对于给定常识三元组和一个linguistic graph，Pattern Extraction的目标是找到一种基于语言关系的模式，这样，给定r，我们就可以准确地从G中提取h和t中的所有单词。
- Pattern Selection and Knowledge Extraction：评估pattern的合理性，选出分数大于0.05的
- Commonsense Knowledge Ranking： 为了最小化模式噪声的影响，我们提出了一个基于置信度的知识排序模块，对所有提取的知识进行排序。 为此，我们首先使用人类注释器来标记一个微小的  提取的知识子集，然后使用它训练分类器。 我们通过学习的分类器为每个提取的知识分配一个置信度分数。

# 实验过程
1. 与baseline比较
2. case study
3. 下游任务评估

# 论文亮点
使用下游任务评估
