# 论文目的
实现常识问答——常识问答要用到外部知识，现有的常识问答方法有两种：they either generate evidence from human-annotated evidence or extract evidence from a homogeneous knowledge source like structured knowledge ConceptNet. 但是they fail to take advantages of both knowledge sources simultaneously.

# 论文方法
Our approach consists of two parts: knowledge extraction and graph-based reasoning
## knowledge extraction
原文：extract knowledge from structured knowledge base ConcpetNet and Wikipedia plain texts according to the given question and choices.We construct graphs to utilize the relational structures of both sources.  
### 从conceptnet中抽取知识
对于每个问题和选择，我们在conceptnet图中定义它们的实体。然后从问题实体到选择实体找出至少三条路，然后构成graphs

### 从Wikipedia中抽取知识
先把问题和选择中的停用词去除，拼接后查询，搜索前K名的作为证据，证据按照eSemantic Role Labeling (SRL)方法结构化构图。

## graph-based reasoning
原文: we propose two graph-based modules which consists of a graph-based contextual word representation learning module and a graph-based inference module to infer final answers

### graph-based contextual representation learning module
借助图信息学习文本word表示重新定义word距离

### graph-based inference module
通过图卷积网络，利用邻居信息获得节点表示，并且汇总图表示推测结果
# 实验方法
## baseline
For the compared methods, we select models and classify them into 4 groups.   
Group 1: models without descriptions or papers,   
Group 2: models without extracted knowledge,  
Group 3: models with extracted structured knowledge and  
Group 4: models with extracted unstructured knowledge.  

## 实验内容
1. 在CommonsenseQA上对比baseline效果
2. Ablation Study——对比模型简化版本以证明每个模块的有效性
3. case study
4. 误差分析——the lack of evidence, similar evidence and dataset noise


# 论文亮点
实验做得极其充分
