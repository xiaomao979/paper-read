# 论文目的
生成对话系统总会产生无意义的对话，例如“我不知道”，所以本论文利用常识来补充对话背景信息，为对话增添色彩
# 论文方法
D为训练集，X为查询信息，Y为回应内容，F为常识知识
## Felicitous Fact mechanism
- Knowledge Retriever:检索查询实体，获取邻居信息构成KG
- Context Encoder:使用双向GRU，输入XorY，输出文本状态序列
- Felicitous Fact Recognizer:区分歧义词
- Context-Knowledge Fusion:加强decoder对背景知识的理解

## Triple Knowledge Decoder
Decoder端是另一个GRU网络,在每一时刻,decoder端可以生成vocabulary words, knowledgeable entity words和copied words中的其中一个.

# 实验方法
## dataset
- English Reddit dataset
- Chinese Weibo dataset
## baseline
For the compared methods, we select models and classify them into 4 groups.   
Group 1: models without descriptions or papers,   
Group 2: models without extracted knowledge,  
Group 3: models with extracted structured knowledge and  
Group 4: models with extracted unstructured knowledge.  

## 实验内容a
1. 在CommonsenseQA上对比baseline效果
2. Ablation Study——对比模型简化版本以证明每个模块的有效性
3. case studya
4. 误差分析——the lack of evidence, similar evidence and dataset noise


# 论文亮点
1. 实验部分采用多重语言
