转载自https://zhuanlan.zhihu.com/p/81917730
# 论文目的
本文针对的数据集是：CommonsenseQA。使机器具备进行常识推理的能力，减小人机之间的差距。
# 论文理论
提出了一个Knowledge-aware reasoning 框架，主要有以下两个步骤:  
1. schema graph grounding   
2. graph modeling for inference    
提出了一个Knowledge-aware graph network 模块: KAGNET。核心是 GCN-LSTM-HPA 结构：  
1. 由GCN, LSTM, 和 hierarchical path-based attention mechanism组成  
2. 用于 path-based relational graph representation  
主要步骤
1. 首先，分别识别出q和a中提及的 concept ，根据这些 concept ，找到他们之间的路径，构建出 (ground) schema graph；
2. 使用 LM encoder 编码 QA 对，产生 statement vector s，作为 GCN-LSTM-HPA 的输入，来计算 graph vector g ；
3. 最后使用 graph vector 计算最终的QA对的打分
## model
问题q和一个包含N选项的候选答案集{a_i} ,schema graph G(V,E)  
### Schema Graph Grounding
#### Concept Recognition
n-gram 匹配：句子中的 token 和 ConceptNet 的顶点集合进行 n-gram 匹配.Note：从有噪声的知识源中有效地提取上下文相关的知识仍是一个开放问题
#### Schema Graph Construction
sub-graph matching via path finding
采取一种直接有效的方法：直接在Q和A中提及的Concept (Cq U Ca) 之间查找路径.  
对于问题中的一个 Concept ci \in Cq 和候选项中的一个 Concept cj \in Ca ，查找他们之间路径长度小于k  的path，添加到图中
#### Path Pruning via KG Embedding
为了从潜在噪声的schema graph中删除无关的path
1. 使用KGE方法（如TransE等）预训练Concept Embedding和Relation Type Embedding（同时可用于KAGNET的初始化）
2. 评价路径的质量.将路径分解为三元组集合，一条路径的打分为每一组三元组的乘积，通过设置一个阈值进行过滤。 三元组的打分通过KGE中的打分函数进行计算（例如，the confidence of triple classification）

具体公式难以编辑，可以去原文查看
# 实验缺陷
negative reasoning
graph grounding 对否定词不敏感  
comparative reasoning strategy——没有进行答案之间的比较  
subjective reasoning——有些答案是根据带有主观性的推理得到的  


