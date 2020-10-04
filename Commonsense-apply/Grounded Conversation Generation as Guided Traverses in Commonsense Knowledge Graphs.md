# 论文目的
用常识性知识图显式地建模会话流
# 论文方法
通过将对话与概念空间联系起来，ConceptFlow将潜在的对话流表示为沿着常识关系在概念空间中遍历。
## 任务描述
user输入话语X（有m个单词），对话生成模型使用encoder-decoder框架产生回答
## Concept Graph Construction
先找到出现在对话里的概念V_0，然后再去常识库找到1-hop和2-hop的邻居V_1和V_2，V_0到V_1形成central concept graph G_central（与当前对话主题相近），V_1到V_2形成outer graph G_outer。

## Encoding Latent Concept Flow
从当前对话出发，遍历G_central和G_outer
- Central Flow Encoding ：G_central被GNN编码后产生信息
- Outer Flow Encoding ：使用attention机制，融合V_1和V_2对应的概念embedding

## Generating Text with Concept Flow
为了同时考虑用户话语和相关信息，解码器使用两个组件来合并来自用户话语和潜在概念流的文本：1）结合其编码的上下文表示。 2）从上下文表示中条件生成单词和概念。
- Context Representation ：使用GRU得到output context representation s_t, 即s_t = GRU(s_t-1, c_t-1 * y_t-1), y_t-1 是上一步生成的内容的embedding，c_t-1是综合上一步的文本表示和概念表示。
- Generating Tokens ：使用s_t decode


# 实验内容
## Dataset
使用Reddit数据集
## baseline
- standard Seq2Seq
- knowledge enhanced ones
- fine-tuned GPT-2 systems

## 实验过程
五类实验
- Response Quality ： 使用自动评估和人类评估来比较conceptflow和其他baseline
- Effectiveness of Multi-hop Concepts ：考虑hop因素，考察考虑G_central 与 同时考虑G_central和G_outer的区别
- Hop Steps in Concept Graph：考虑hop因素，考察更多hop对结果的影响（e.g. 3-hop）
- Case Study
- Learned Attentions on Concepts ：探究conceptflow更多的使用了哪种hop对应的概念

# 论文亮点
1. 实验充分
