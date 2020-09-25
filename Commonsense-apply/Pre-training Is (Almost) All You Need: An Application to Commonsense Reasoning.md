
# 论文目的
对于分类问题or句子拼接问题而言，预训练模型可能会由于没有任何先验知识而导致次优解，为了解决这个问题，作者使用full-text技术提高了准确率

# 论文方法
句子拼接问题——[CLS] premise [SEP] hypothesis [SEP]
## full-text
作者将两个句子的拼接形式从 
- [CLS] premise [SEP] hypothesis [SEP] 

改为 


- [CLS] premise 连接词 hypothesis [SEP]

## N-grams sequence scoring
将原始的单个单词概率分数转为n-gram形式,即，
- P (p(k) | s_i\p(k)) 和 P (h_i(k) | s_i\h_i(k)) 

改为  

- P (p(k:k+g-1) | s_i\p(k:k+g-1)) 和 P (h_i(k:k+g-1) | s_i\h_i(k:k+g-1))
