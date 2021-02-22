# 摘要
我们描述了一个单一的卷积神经网络体系结构，给定一个句子，它会输出大量的语言处理预测：part-of-speech tags, chunks, named entity tags, semantic roles, semantically similar words and the likelihood that the sentence makes sense (grammatically and semantically) 。使用权重共享（多任务学习的一个实例）对整个网络进行所有这些任务的联合培训。除了从未标记文本中学习的语言模型外，所有任务都使用标记数据，并且语言模型代表共享任务的一种新型半监督学习semi-supervised learning形式。我们展示了多任务学习和半监督学习如何提高共享任务的泛化能力，从而实现最先进的性能。

#  NLP Tasks
- part-of-speech tagging：对具体的句子中的单词进行标注，例如，Plays/VBZ well/RB with/IN others/NNS
- chunks：从非结构化文本中提取短语的过程
- parsing：句法分析，指对句子种的词语语法功能进行分析
- anaphora resolution：指代消解
- word-sense disambiguation：词义消歧
- semantic-role labeling：语义角色标注，给定一个句子， SRL 的任务是找出句子中谓词的相应语义角色成分，包括核心语义角色（如施事者、受事者等） 和附属语义角色（如地点、时间、方式、原因等）。根据谓词类别的不同，又可以将现有的 SRL 分为动词性谓词 SRL 和名词性谓词 SRL。
- word-stemming：抽取词的词干或词根形式

# General Deep Architecture for NLP
- Transforming Indices into Vectors：将单词映射为向量表示
- Variable Sentence Length： normal NNs无法解决句子长度变化的问题，虽然window approach可以解决一部分简单的问题，但是对于长距离依赖的问题依然不适用， 因此使用Time-Delay Neural Networks (TDNNs)解决，即使用CNN
- Deep Architecture：使用激活函数加深神经网络

# Multitasking with Deep NN
Multitask learning (MTL) is the procedure of learning several tasks at the same time with the aim of mutual benefit.
## Deep Joint Training：
共享deep layers，即共享 sharing the lookup-tables of each considered task。  
1. Select the next task.
2. Select a random training example for this task. 
3. Update the NN for this task by taking a gradient step with respect to this example. 
4. Go to 1.
## Previous Work in MTL for NLP
- Cascading Features：先训练一个任务，然后把这个任务得到的特征用到下一个任务当中。会导致“一步错，步步错”
- Shallow Joint Training：对于同一个数据集，一个模型同时预测多个任务的标签。但是联合标注数据集很难获取。

# Leveraging Unlabeled Data
对于没有标签的数据，看窗口当前单词是否与context相关（二分类任务）
