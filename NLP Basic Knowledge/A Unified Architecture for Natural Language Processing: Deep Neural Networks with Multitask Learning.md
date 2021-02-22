# 摘要
我们描述了一个单一的卷积神经网络体系结构，给定一个句子，它会输出大量的语言处理预测：part-of-speech tags, chunks, named entity tags, semantic roles, semantically similar words and the likelihood that the sentence makes sense (grammatically and semantically) 。使用权重共享（多任务学习的一个实例）对整个网络进行所有这些任务的联合培训。除了从未标记文本中学习的语言模型外，所有任务都使用标记数据，并且语言模型代表共享任务的一种新型半监督学习semi-supervised learning形式。我们展示了多任务学习和半监督学习如何提高共享任务的泛化能力，从而实现最先进的性能。
- part-of-speech tagging：对具体的句子中的单词进行标注，例如，Plays/VBZ well/RB with/IN others/NNS
- chunks：从非结构化文本中提取短语的过程
- parsing：句法分析，指对句子种的词语语法功能进行分析
- anaphora resolution：指代消解
- word-sense disambiguation：词义消歧
- semantic-role labeling：语义角色标注，给定一个句子， SRL 的任务是找出句子中谓词的相应语义角色成分，包括核心语义角色（如施事者、受事者等） 和附属语义角色（如地点、时间、方式、原因等）。根据谓词类别的不同，又可以将现有的 SRL 分为动词性谓词 SRL 和名词性谓词 SRL。

# 
