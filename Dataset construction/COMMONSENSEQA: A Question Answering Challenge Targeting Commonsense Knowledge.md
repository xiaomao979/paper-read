# 论文目的
构建常识问答数据集，该数据集的特点是：
1. 问题可以不经过文本而轻易地根据常识被人类回答
2. 最先进的预训练语言模型也无法取得很好的效果，而人类可以轻而易举的取得很好的效果
# 论文方法
向crowd workers提出问题，以描述来自CONCEPTNET的概念之间的关系，构建过程如下（figure 1）：  
- A source concept (in green) and three target concepts (in blue) are sampled from CONCEPTNET (b) Crowd-workers generate three questions, each having one of the target concepts for its answer (✓), while the other two targets are not (✗). Then, for each question, workers choose an additional distractor from CONCEPTNET (in red), and author one themselves (in purple)

## 具体过程
1. 我们从CONCEPTNET中提取子图，每个子图具有一个源概念和三个目标概念。
2. 我们要求众包工作者在每个子图中提出三个问题（每个目标概念一个），为每个问题添加两个额外的干扰因素，并验证问题的质量。
3. 我们通过查询搜索引擎并检索网络摘要来为每个问题添加文本上下文。

也就是说：一个问题，5个答案，分别为
- 主观拟写干扰答案，
- 从conceptnet中挑选干扰答案（必须有相同的relation），
- 原有关系三个答案，其中一个是符合题意的，另外两个因为不符合题意，故而都是干扰答案

## 添加文本
向Google搜索发出一个针对每个问题和候选答案的网络查询，并将该问题和答案串联起来。 为五个答案候选者中的每个候选者获取前100个结果片段，每个问题的上下文为500个片段。 使用此上下文，我们可以研究COMMONSENSEQA上的阅读理解（RC）模型的性能。

# 实验过程
## baseline
两类模型
- 是否被训练
- 是否用到上下文

## 实验setup
8:1:1分为训练集，验证集和测试集，有两种分隔方法
- 随机分隔——效果很不好，因为相同的问题概念出现在不同集合中却出现了不同的答案概念，机器无法学习
- 三组中的每组都有不相交的问题概念

既然随机分隔效果很不好，我们就应该把它当作首选分隔方法，因为对于我们的目标来说，我们就是让机器学习不好而人类轻易解决。

为了理解我们任务的难度，我们还用了SANITY mode，即把从conceptnet中挑选干扰答案（必须有相同的relation），换成随机选择干扰项进行实验

## 实验结果
BERT-LARGE表现最好，对其进行分析发现,在表面线索暗示正确答案的例子上，该模型表现得很好(77.7%的准确率)。
包含否定或理解反义词的例子(42.8%)和类似于需要事实性知识的例子(38.4%)准确率较低，当正确答案的粒度比干扰物的一个粒度更细时(35.4%)和当正确答案需要满足几个条件，而干扰物只满足其中一个条件时(23.8%)时准确性尤其低。
