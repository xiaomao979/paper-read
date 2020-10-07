# 论文目的
利用主题常识知识来丰富对话内容
# 论文方法
## 任务描述
令X表示查询消息，Y表示目标响应，F = {f}表示从常识图G中检索到的一组事实，而ft表示主题事实。 每个事实都组织成一个SVO（主语，谓语，宾语）三元组，即f =（e1，r，e2）。 代替将对话生成建模为P（Y | X），TopicKA同时生成以查询消息和推荐主题事实为条件的响应。 即，P（Y | X，ft）
## Method
- Context Encoder：双向GRU网络编码对话内容U，得到隐层状态Hu
- Topic Fact Recommender：借助Hu，ft从检索到的知识事实中被挑选出来，fi被推荐作为主题事实的概率借助softmax实现。
- Topic Fact Diffusion Network：一个事实通常不足以涵盖一个主题的知识。 因此，我们设计了一个主题事实扩散网络，以基于ft检索更多相关事实。
-  Integration Schemes： 生成网络需要一个离散的分类主题事实作为输入，这意味着我们需要从推荐网络输出的分布中采样一个主题事实
# 实验内容
1. 与baseline比较
2. 消融实验
3. case study
