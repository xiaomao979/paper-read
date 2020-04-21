# 论文目的
在MIL和PCNN的基础上，利用句子级别的注意力机制进行加权，用于关系抽取

# 论文理论
MIL——给定一组句子，每个句子有相同的头实体和尾实体，给定一组候选关系集合，模型给出这组句子表达关系的概率  

sentence encoder——CNN/PCNN  
selective attention over instances——生成句子级别的权重以帮助去噪  

word和position拼接后（cat）然后转化为词向量——保存了句子的结构信息  
PCNN的P指在max-pooling分段处理，取每一段的max-pooling结果拼接——防止丢失过多有用的信息，对结构信息进行更好的把控  

一组句子的表示得到一个总体表示——对每个句子进行一个加权处理（这个权重可以应用到注意力机制）  

# 实验方法
横向比较，本文加了attention的CNN/PCNN的方法，是否明显优于其他模型
