# 论文目的
 现有的方法将常识知识整合到生成的预先训练的语言模型中，只是通过在单个知识三元组上的后训练来传递关系知识，而忽略知识图中丰富的连接关系。在本文中，我们提出了使用多跳推理流程（GRF）进行生成的方法，该方法可以在从外部常识知识图中提取的多关系路径，启用带有动态多跳推理的预训练模型。
# 论文方法
## 任务描述
输入一段文本，输出一段生成的文本（类似于生成故事结尾）。
## Method
为了利用推理过程，我们需要从知识图谱当中抽取一个子图，子图为原始概念+h-hop邻居信息 
### Generation with Multi-Hop Reasoning Flow
- Static Multi-Relational Graph Encoding：使用GNN获取图编码
- Context Modeling with Pre-Trained Transformer：使用GTP-2获取文本内容信息
- Dynamic Multi-Hop Reasoning Flow：
