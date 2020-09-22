# 论文目的
物理问题很难从文本当中习得，本篇论文观察了AI（主要是预训练的语言模型）是否可以学会在不经历物理世界的情况下可靠地回答物理常识问题。
本论文最大的贡献是构建了物理数据集PIQA

# 论文方法
## Dataset Construction
借助于教人们怎么使用各种东西的网站，构建数据集。数据分为三部分
- physical goal
- solution
- topically related trick: 给出一个和solution相近但是错误的答案

## AFLite algorithm
AFLite algorithm用于从数据中删除样式工件和琐碎的示例。AFLite使用在数据的随机子集上训练的一组线性分类器来确定这些预先计算的嵌入是否是正确答案选项的有力指标。 不必专门确定偏差的可能来源，该方法通过依靠最新技术来发现不希望的注释伪像，从而实现无监督的数据偏差减少。


# 实验方法
使用预训练模型看是否模型可以解决PIQA
## Model
- GPT
- Bert
- RoBERTa

## 实验结果

 
Model | Size | Validation Acc |  Test Acc  
 ---- | ----- | ------   | ------ 
GPT | 124M | 70.9 | 69.2  
BERT | 340M | 67.1  | 66.8  
RoBERTa | 355M | 79.2 | 77.1  

可以看出效果并没有很理想


