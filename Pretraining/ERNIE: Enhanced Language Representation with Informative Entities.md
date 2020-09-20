参考：https://blog.csdn.net/herosunly/article/details/90901995
# 摘要
NLP表示模型如BERT的预训练模型能够在大量的纯文本语料中捕获丰富的语义信息，并且通过微调改进NLP任务的效果。然而，已存在的预训练语言模型很少考虑将知识图谱的结构化信息融入其中，从而提高语言的理解。我们认为知识图谱中的信息实体能够增强语言表示。在这篇论文中，我们利用了大规模的语料信息和知识图谱，去训练一个增强的语言表示模型，它能够同时利用词汇、语义和知识信息。实验结果表明了ERNIE效果很好，在各项知识驱动的任务中都超过了BERT模型。源代码地址为： https://github.com/thunlp/ERNIE 

# 论文目的
要将外部知识组合到语言表征模型中，我们又会遇到两大主要挑战：  
- 结构化的知识编码：对于给定的文本，如何高效地抽取并编码对应的知识图谱事实是非常重要的，这些 KG 事实需要能用于语言表征模型。
- 异质信息融合：语言表征的预训练过程和知识表征过程有很大的不同，它们会产生两个独立的向量空间。因此，如何设计一个特殊的预训练目标，以融合词汇、句法和知识信息就显得非常重要了。

为了克服上面提到的这些挑战，清华大学等研究者提出一种名为通过多信息实体增强语言表征（ERNIE）的模型。重要的是，ERNIE 能同时在大规模文本语料库和知识图谱上预训练语言模型。

# 论文方法
对于抽取并编码的知识信息，研究者首先识别文本中的命名实体，然后将这些提到的实体与知识图谱中的实体进行匹配。研究者并不直接使用 KG 中基于图的事实，相反他们通过知识嵌入算法（例如 TransE）编码 KG 的图结构，并将多信息实体嵌入作为 ERNIE 的输入。基于文本和知识图谱的对齐，ERNIE 将知识模块的实体表征整合到语义模块的隐藏层中。  

与 BERT 类似，研究者采用了带 Mask 的语言模型，以及预测下一句文本作为预训练目标。除此之外，为了更好地融合文本和知识特征，研究者设计了一种新型预训练目标，即随机 Mask 掉一些对齐了输入文本的命名实体，并要求模型从知识图谱中选择合适的实体以完成对齐。现存的预训练语言表征模型只利用局部上下文预测 Token，但 ERNIE 的新目标要求模型同时聚合上下文和知识事实的信息，并同时预测 Token 和实体，从而构建一种知识化的语言表征模型。  

模型将BERT中的Encoder替换为了T-Encoder+K-Encoder，T-Encoder依然是对原来的文本进行编码，这部分和BERT是一样的，在K-Encoder中，可以看到输入输出都变成了两个，多了entity的信息。具体来说，首先可以利用TransE的方法对知识图谱中的内容进行表示，并对文本中的实体进行识别，这样文本中的实体都会有一个来自知识图谱的实体表示，需要注意的是文本的长度和实体的长度并不相等，然后先用mutli-head attention对文本和实体分别进行处理，得到在整个序列中情境感知的语义表示接下来就是对这两种信息进行融合，或者说利用实体的信息来增强对文本语义的理解，这个时候就分成两种情况：- 文本中的词有实体对应，一个很简单的思路，通过一个非线性变换，得到融合后的信息 - 文中的词没有实体对应，为了保证一致性，还是同样的方法，只是只有实体词的输入。通过这样的方法，就将实体的知识信息融入到了对文本语义的增强表示中，接下来将相应的单元重复多次，就得到的最终的文本语义表示。



# 训练过程
dEA的目的就是要求模型能够根据给定的实体序列和文本序列来预测对应的实体

这个公式也被当作训练dEA时的损失函数，有了目标，那么数据该如何准备呢？和Masked Language Model类似，作者对实体也做了如下处理：  
1. 对于一个给定的文本-实体对应序列，5%的情况下，实体会被替换为一个随机的实体，这么做是为了让模型能够区分出正确的实体对应和错误的实体对应；  
2. 对于一个给定的文本-实体对应序列，15%的情况下，实体会被mask，这是为了保证模型能够在文本-实体没有被完全抽取的情况下找到未被抽取的对应关系；  
3. 对于一个给定的文本-实体对应序列，剩下的80%的情况下，保持不变，这是为了保证模型能够充分利用实体信息来增强对文本语义的表达。  


在 BERT 模型中，通过『哈』与『滨』的局部共现，即可判断出『尔』字，模型没有学习与『哈尔滨』相关的知识。而 ERNIE 通过学习词与实体的表达，使模型能够建模出『哈尔滨』与『黑龙江』的关系，学到『哈尔滨』是 『黑龙江』的省会以及『哈尔滨』是个冰雪城市。