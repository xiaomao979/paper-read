# 论文目的
使用小样本自监督学习方法来解决Pronoun Disambiguation 和 Winograd Schema Challenge problems。引入了成对水平的互斥损失（a pair level
mutual-exclusive loss），以在表征学习中增强常识知识

# 论文方法
## mutual-exclusive loss
假设成对代词消歧是相互排斥的。mutual-exclusive loss = L_ME +L_CM。

- L_ME 为跨对答案的互斥性
- L_CM 为在语言模型的候选可能性之间建立了余量


