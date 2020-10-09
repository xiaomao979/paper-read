# 论文目的
调查研究了预训练模型是否可以得出数字常识知识，若可以那么可以理解到什么程度，以及该过程的鲁棒性，同时构建了数字常识知识数据集NUMERSENSE

# NUMERSENSE构建过程
- 从OMCS抽取含{“no”, “zero”, “one”, “two”, ..., “ten” }其中任意一个单词的句子。 为了降低噪音，作者手工和务实地修改了这些句子，并由不同的研究生进行了两轮审查，作者只保留了所有注释者接受的陈述。
- 为了检测模型的鲁棒性， 我们还在我们的数据集添加了对抗性的例子，即在每个检测中涉及数值推理的名词之前添加形容词
- 作者还手动注释了每个实例的类别标签，以便能够更好地理解所涵盖的主题及其百分比

# 检验过程
1. 使用最先进的预训练模型（BERT,RoBerta,GPT2)进行实验
2. 改成问答模型，使用最先进的commonsenseQA模型进行实验