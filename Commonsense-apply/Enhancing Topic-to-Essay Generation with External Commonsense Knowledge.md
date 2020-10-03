# 论文目的
自动 topic-to- essay 生成（TEG）任务是指给定 topic 集合，生成主题相关、段落集的文本。过去的工作仅仅基于给定的主题去执行文本生成，而忽略了大量的常识知识，其实这些常识知识会提供额外的背景知识，这能提高生成文章的新颖性和多样性。为了解决这个问题，本文通过动态记忆机制将外部知识库的知识整合进生成器。除此之外，基于多标签判别器的对抗训练的应用进一步提高了主题一致性。

# 论文方法
## 任务描述
 给定一个包含m个主题的主题序列x，TEG任务旨在生成一个包含n个单词的主题一致的文章y，其中n远大于m。
## Memory-Augmented Generator
大体上为encoder-decoder
### Encoder
encoder端为LSTM模型，融合主题信息，得到hidden states
### Decoder
利用ConceptNet知识库，查询得到主题对应的邻居信息，并获取预先训练好的词向量构成记忆矩阵M，将记忆矩阵加入decoder中
### Dynamic Memory
随着生成的进行，需要表达的主题信息不断变化，这就需要动态更新记忆矩阵。
- M^i_t* = tanh (U_1M^i_t + V_1e(y_t))
- g^i_t = sigmoid(U_2M^i_t + V_2e(y_t))
- M^i_t+1 = (1 − g^i_t) . M^i_t + g^i_t .M^i_t*
