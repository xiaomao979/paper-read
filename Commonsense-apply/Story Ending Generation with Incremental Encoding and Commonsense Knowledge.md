# 论文目的
利用常识知识来生成故事结尾
# 论文方法
## 任务描述
给定句子个数为K的story文本，生成一个句子长度为l的结尾（结尾的句子个数为1）
## Method
### incremental encoding scheme
当encoding当前句子X_i时，它获取一个对前面句子X_{i-1}的仔细阅读上下文向量。以这种方式，我们可以隐式捕获相邻句子之间单词的order/relationship
### Multi-Source Attention
内容向量由两部分组成， 他们都是通过MSA求得的。第一个是通过处理前一句的隐藏状态来导出的（state context vector），第二个是通过处理表示前一句的1-hop的知识图向量来导出的（knowledge context vector）。
### Knowledge Graph Representation
 一个句子中的每个单词都被用作一个查询，从常识知识图谱中检索一个1-hop图
# 实验内容
## Dataset
ROCStories
