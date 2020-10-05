# 论文目的
利用常识知识来选择故事结尾
# 论文方法
## 任务描述
给定句子长度为L的故事S，我们的任务是在两个候选答案中选出正确的从而使得故事更为合理和一致。其实是0 or 1二分类问题
## method
三部分组成  
- narrative sequence
- sentiment evolution
- structured commonsense knowledge
### Narrative Sequence
 为叙事链开发更好的语义表示对于我们预测正确的结局是很重要的。作者在一个无标签的大数据语料集上预训练一个高度兼容的语言模型来学习文本隐藏信息。将训练好的语言模型利用transform结构迁移到我们的任务当中。计算语义连贯性得到最终0 or 1概率
### Sentiment Evolution
考虑到故事在情感方面与其他文本不同，我们预训练一个情感预测模型：
1. 将训练样本的故事分为五个部分，利用VADER工具，获取每个部分的情感向量E_i（positive, negative or neutral）  
2. 利用LSTM模型编码句子情感和文本得到hidden state h_i，并使用激活函数的得到第五个的预测情感向量E_p  
3. 计算第五个的预测情感向量E_p与第五个的真实情感向量E_5的cosine相似度作为训练过程。  
将训练好的模型应用在测试文本上得到整个故事的预测情感向量E_p，同时获得候选答案的预测情感向量，利用softmax + 二次型得到最终0 or 1概率。
### Commonsense Knowledge
给定故事体，候选集和标签，我们使用NLTK对他们进行tokenize和去停用词，计算候选结局和故事的知识距离向量。
### Combination Gate
最后综合上述三种计算结果

# 实验内容
## Dataset
使用ROCStories
## 实验过程
- baseline
- 消融实验
- casestudy

# 论文亮点
1. 三个部分是并行的
