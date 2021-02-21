# 摘要  
我们提出了CODEX，这是一组从Wikidata和Wikipedia提取的知识图谱补全（knowledge graph completion）数据集，它们在难度和范围上改进了现有知识图谱补全基准。就范围而言，CODEX包括三个大小和结构各异的知识图谱，实体和关系的多语言描述，以及成千上万个合理但被证实为假的难负样本（hard negative）三元组。为了表征CODEX，我们提供了详尽的经验分析和基准测试。首先，我们根据逻辑关系模式分析每个CODEX数据集。接下来，我们针对五个经过广泛调整的KG嵌入模型在CODEX上报告基准链接预测和三元组分类结果。最后，我们通过显示CODEX涵盖了更多样化和可解释的内容，并且它是一个更困难的链接预测基准，将CODEX与流行的FB15K-237知识图谱补全数据集区分开。（ps：FB15k-237是Freebase的子集，包含237种关系和14k种实体。Freebase是个类似wikipedia的创作共享类网站，所有内容都由用户添加，采用创意共用许可证，可以自由引用。两者之间最大的不同在于，Freebase中的条目都采用结构化数据的形式，而wikipedia不是。）

# Introduce
从freebase中抽取数据来实现知识图谱补全会存在质量问题，作者提出了CODEX：a set of knowledge graph COmpletion Datasets EXtracted from Wikidata and its sister project Wikipedia

# Existing datasets
介绍了从Freebase知识图谱和其他知识图谱抽取得到的数据集

# Data collection  
1. 使用Snowball sampling获取初始样本（PS：滚雪球抽样（Snowball sampling）滚雪球抽样是指先随机选择一些被访者并对其实施访问，再请他们提供另外一些属于所研究目标总体的调查对象， 根据所形成的线索选择此后的调查对象。 例如，要研究退休老人的生活， 可以清晨到公园去结识几位散步老人，再通过他们结识其朋友， 不用很久，你就可以交上一大批老年朋友。 但是这种方法偏误也很大，那些不好活动、不爱去公园、 不爱和别人交往、喜欢一个人在家里活动的老人， 你就很难把雪球滚到他们那里去， 而他们却代表着另外一种退休后的生活方式。）  
2. 然后我们构建知识图谱，并去除度小于K的，以“create smaller data snapshots”，并去除双向边。最后分隔90/5/5 train/validation/test triples
3. 并借助Wikidata和Wikipedia，为知识图谱增加额外信息。
4. 手动构建难度较高的负样本：利用预训练语言模型预测三元组的尾实体，并去top10不在KG中的，并手动标注获取负样本

# Analysis of relation patterns
分析了CODEX中的三类关系symmetry,inversion, and compositionality  
1. symmetry：（h, r, t) in G implies (t, r, h) in G  
2. Compositionality：A=B，B=C -> A=C  
3. inversion忽略是为了防止train/test leakage（PS：数据泄漏是指机器学习模型的创建者在测试数据集和训练数据集之间意外地共享信息所犯的错误。通常，当将数据集分割为测试集和训练集时，目标是确保两者之间没有数据共享。）  

# Benchmarking
我们在link prediction and triple classification上对CODEX进行基准测试（运用了五个模型：RESCAL, TransE, ComplEx, ConvE, and TuckER）。    
1. Link prediction：给定其中一个实体和关系，预测另一个
2. triple classification：预测真假

#  Comparative case study
比较了CODEX-M and FB15K-237数据集，证明CODEX在多样性，可解释性上都较为优秀
