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
## Multi-Label Discriminator
引入鉴别器D来评价输入主题与生成的文章之间的主题一致性，进一步提高了文本质量。鉴别器是X+1分类，区分是属于X个 topic 还是属于生成样本
## Adversarial Training
Our generator G can be viewed as an agent, whose state at time step t is the current generated words y1:t−1 = (y1, ··· , yt−1) and the action is the prediction of the next word yt。

# 实验内容
## Dataset
使用知乎数据集
## Evaluation Metrics
使用两种评估方法——自动评估和人类评估
### Automatic Evaluation
- consistency ： 一个好的essay应该与所有主题语义相近。使用SGM预训练好的多标签分类器，使用jaccard相似方程来计算生成文本主题和原始主题的consistency得到矩阵
- Novelty ： 新颖性可以通过看看生成文本与训练文本的区别来判定。使用jaccard相似方程来计算生成文本和原始主题文本的consistency得到矩阵
- Diversity ： 我们还计算了不同的n-gram在生成的文章中的比例，以评估输出的多样性。

### Human Evaluation
200个样本（包含输入和输出）分给3个标注者。然后，他们被要求从1到5对生成的文章的的四个标准进行评分：新颖性、多样性、连贯性和主题一致性。 对于新颖性，我们使用TF-IDF特性检索10 最相似的训练样本，为注释者提供参考。

## 实验过程
1. 与baseline比较
2. 消融实验
3. case study

# 论文亮点
1. 评估方式特别——自动与人工两种结合
2. 对抗学习和深度学习结合
