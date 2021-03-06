参考：https://blog.csdn.net/boywaiter/article/details/103982824  

摘要： ConceptNet是一个知识图谱，其中自然语言单词和短语通过带标签（表示边的类型）和权重（表示边的可信程度）的边相互连接。将ConceptNet与词嵌入结合（例如，word2vec），有助于词的相关性评价（使得相关的词的嵌入更接近）。  

# Introduction
ConceptNet用三元组表示断言。  
ConceptNet还用ExternalURL表示与外部知识资源的链接，包括WordNet，Wiktionary，OpenCyc和DBPedia等。  
ConceptNet中的图结构化知识对于NLP学习算法特别有用，尤其是基于词嵌入的算法，例如Mikolov等人，2013。我们可以使用ConceptNet构建比分布式语义更有效的语义空间。  
最有效的语义空间是使用泛化的“翻新（retrofitting）”方法（Faruqui等人，2015），从分布式语义和ConceptNet两者中学习得到的。我们将此混合语义空间称为“ ConceptNet Numberbatch”，以区别于ConceptNet本身。
在词相关性的许多评估中，ConceptNet Numberbatch的性能明显优于其他系统，而性能的提高转化为对下游任务（如类比）的改进。在SAT风格的类比问题语料上（Turney，2006年），其准确率达到56.1％，优于其他基于词嵌入的系统，并与之前最好的整体系统Turney的LRA持平。这种准确性水平仅略低于一般人工测试人员的性能。

# Related Work
ConceptNet是Open Mind常识项目（Singh 2002）的知识图谱版本，是人类所了解的最基本知识的常识知识库。  
Cyc（Lenat and Guha 1989）几十年来建立了谓词逻辑形式的常识知识本体。  
DBPedia（Auer等，2007）从Wikipedia信息框中提取知识，提供了大量事实，主要集中在具有Wikipedia文章的命名实体上。  
Google知识图谱（Singhal，2012年）也许是最大、最通用的知识图谱，尽管其内容不免费提供。它主要关注可消歧的命名实体，其座右铭是“Things, not strings”。  
与其他资源相比，ConceptNet的作用是提供足够大的免费知识图谱，主要关注自然语言中使用的单词（而不是命名实体）的常识含义。对单词的关注使其特别契合将单词含义表示为向量的想法。  
词嵌入将词表示为稠密的（不象one-hot向量那样稀疏）单位实向量，其中紧密靠近的向量在语义上相关。这种表示之所以吸引人，是因为它将含义表示为一个连续的空间，其中相似性和相关性可以视为度量。词嵌入通常作为机器学习任务的副产物，例如根据其邻居预测句子中的某个词。这种关于语义的机器学习方法有时称为分布式语义或分布式词表示，它与语义网络或知识图谱的知识驱动方法形成对比。
嵌入的两个主要矩阵是使用负采样的skip-gram在Google新闻的1000亿个单词上训练的word2vec嵌入（Mikolov等人，2013），以及在8400亿个Common Crawl单词上训练的GloVe 1.2嵌入（Pennington, Socher, and Manning, 2014）。这些矩阵可下载，我们将它们用作比较和集成模型（ensemble）的输入。Levy，Goldberg和Dagan（2015）评估了多种嵌入技术以及各种显式和隐式超参数的影响，使用截短的SVD及其上下文生成了自己的高性能词嵌入，并为词嵌入工程提供了建议。
全息嵌入（Holographic embeddings, Nickel，Rosasco和Poggio 2016）是从带标签的知识图谱中学到的嵌入，但前提是这些嵌入的循环相关性会给出表示关系的向量。这种表示似乎与ConceptNet极为相关。到目前为止，当我们尝试在ConceptNet上实现它时，收敛得太慢，无法进行实验，但是最终可以通过一些优化和附加的计算能力来克服。

# Structure of ConceptNet
## 知识来源
ConceptNet 5.5是从以下来源构建的：  

1. 从开放思想常识（OMCS）（Singh 2002）和其他语言的姊妹项目中获得的事实（Anacleto et al., 2006）
2. 使用自定义解析器（“ Wikiparsec”）从多种语言的解析Wiktionary中提取的信息
3. 旨在收集常识的有目的游戏（冯·安，凯迪亚和布鲁姆，2006年）（中原和山田，2011年）（Kuo等，2009年）
4. 开放式多语言WordNet（Bond和Foster，2013年），WordNet的链接数据表示（Miller等人，1998）及其并行的多语言项目
5. JMDict（布莱恩，2004），日文多语词典
6. OpenCyc，由Cyc提供的上位词层次（Lenat和Guha，1989），代表常识的系统谓词逻辑方面的知识
7. DBPedia的子集（Auer等，2007），是从维基百科信息框中提取的事实网络。

结合这些资源，ConceptNet包含2100万个边和800万个以上的节点。它的英语词汇包含大约1,500,000个节点，并且它包含83种语言，其中每个至少包含10,000个节点。  
Wiktionary是ConceptNet的最大输入来源，它提供1,810万条边，并且主要负责其庞大的多语言词汇。但是，ConceptNet的大部分特性来自OMCS和有目的的各种游戏，这些游戏表达了术语之间的多种不同关系，例如PartOf（“a wheel is part of a car”）和UsedFor（“a car is used for driving”）。

## 关系
ConceptNet所选定关系构成一个封闭类，例如IsA，UsedFor和CapableOf，用于表示独立于其语言的关系或所连接术语的来源。  
ConceptNet 5.5旨在使其知识资源与34个关系（根据版本5.7修改）的核心集合保持一致。这些泛化的关系目的与WordNet的关系（如下位词和别名），以及生成词法理论的本质类似（Pustejovsky 1991）。ConceptNet的边是有向的，但是作为ConceptNet 5.5的一项新功能，某些关系被指定为对称关系，例如SameTo。这些边的方向性不重要。  
核心关系34个（黑体为5.7版本新增，删除线为5.7版本中deprecated）：  
1. Symmetric relations: Antonym, DistinctFrom, EtymologicallyRelatedTo,  EtymologicallyDerivedFrom, LocatedNear, RelatedTo, SimilarTo, and Synonym  
2.  Asymmetric relations: AtLocation, CapableOf, Causes, CausesDesire, CreatedBy, DefinedAs, DerivedFrom, Desires, Entails, ExternalURL, FormOf, HasA, HasContext, HasSubevent, HasFirstSubevent, HasLastSubevent, HasPrerequisite, HasProperty, IsA, MadeOf, MannerOf, MotivatedByGoal, ObstructedBy, PartOf, ReceivesAction, SymbolOf, and UsedFor   

这些关系的定义和示例出现在ConceptNet 5.5文档（https://github.com/commonsense/conceptnet5/wiki/Relations）的页面中。具有特定语义的关系（例如，UsedFor和HasPrerequisite）倾向于连接常见的单词和短语，而稀有词则通过更通用的关系（例如，Synonym和RelatedTo）连接。
如图1所示，在一个可浏览的界面中，ConceptNet中的边按自然英语表示的关系进行分组。  
## 术语表示
ConceptNet以标准化形式表示术语。使用Python的unicodedata实现，将文本标准化为NFKC格式（http://unicode.org/reports/tr15/），再转换为小写，并使用Python程序包wordfreq（Speer等人，2016）中的tokenizer（或者UNIX中的tr -sc 命令）将其拆分为非标点符号（token），该软件包基于标准Unicode单词分段算法。标记用下划线连接，并且该文本前面加URI /c/lang/，其中lang是该术语所用语言的BCP 47语言代码（https://tools.ietf.org/html/bcp47）。例如，英文术语“United States”变为/c/en/united_states。  
关系具有以/r开头的URI的独立命名空间，例如/r/PartOf。这些关系用英语人工命名，但适用于所有语言。葡萄牙语获得的名为“ O alimento e usado para´comer”的语句仍以/r/UsedFor关系表示。  
与ConceptNet 5.4及更早版本相比，最重要的变化在于术语的表示形式。 ConceptNet 5.4要求英语的术语必须采用词元形式（lemmatized  form），因此，例如，“United States”必须表示为/c/en/unite_state。在此表示形式中，“drive”和“driving”是同一术语，使得断言（car，UsedFor，driving）和（drive，HasPrerequisite，have license）相关联。ConceptNet 5.5删除了lemmatizer，而是使用FormOf关系来关联词的词尾变化。现在，上面的两个断言由第三个断言（driving，FormOf，drive）连接，并且“driving”和“drive”都可以在ConceptNet中找到。
## 词汇表
在构建知识图谱时，节点应表示的内容对图的使用方式有重大影响。它还有其他影响，可能使链接和导入其他资源变得不容易，因为不同的资源会对它们的表示方式做出不同的决定。  
在ConceptNet中，节点是自然语言的单词或短语，通常是未消歧的常见单词。英文中的“lead”一词是ConceptNet中的一个术语，由URI  /c/en/lead表示，即使它具有多种含义。歧义术语的优点是可以轻松地从有歧义的自然语言中提取它们。这种歧义表示等同于从文本中学习分布语义的系统所使用的表示。  
ConceptNet的表示允许使用术语的更具体、明确的版本。URI /c/en/lead/n指的是“ lead”一词的名词含义，当搜索或遍历ConceptNet时，该URI有效地包含在/c/en/lead中，并通过隐式关系SenseOf与之链接。许多数据源提供有关词性的信息，使我们可以将其用作提供少量歧义的常见表示形式。URI结构允许进一步消除歧义，但目前尚不使用。  
## 链接数据
ConceptNet从其他系统（如WordNet）中导入知识到其自己的表示形式中。这些其他系统有其自己的目标词汇表，需要与ConceptNet对齐，这通常是未指定的多对多对齐方式。  
从另一个知识图谱导入的术语将通过关系ExternalURL连接到ConceptNet节点，指向表示该外部资源中该术语的绝对URL。这种新引入的关系保留了数据的来源，并允许查找未转换的数据是什么。ConceptNet术语也可以表示为绝对URL，因此这使ConceptNet可以双向连接到更广泛的链接开放数据生态系统。  

# 将ConceptNet应用于词嵌入
## 使用PPMI计算ConceptNet嵌入
我们可以将ConceptNet图表示为稀疏、对称的术语-术语矩阵。矩阵的每个元素包含连接两个相应术语的所有边的权重之和。出于性能原因，在构建此矩阵时，我们通过丢弃连接到少于三个边的术语来修剪ConceptNet图。  
我们认为此矩阵代表术语及其上下文。在文本语料库中，术语的上下文是出现在文本附近的术语。在这里，上下文是ConceptNet中与其相连的其他节点。我们可以遵循Levy，Goldberg和Dagan（2015）的实际建议，直接从这个稀疏矩阵中计算词嵌入（不采用神经网络的方法的原因是，Levy等人发现，词嵌入的许多性能提升是由于某些系统设计选择和超参数优化，而不是嵌入算法本身。 此外，我们证明了这些修改可以转移到传统的分布式模型中，从而获得相似的收益。 与以前的报告相比，我们观察到这些方法之间的性能差异主要是局部的或微不足道的，没有任何一种方法比其他方法具有全局优势。）。  
与Levy等人一样，我们使用上下文分布平滑确定矩阵项的逐点互信息，裁剪负值以产生正逐点互信息（positive pointwise mutual information, PPMI），使用截断SVD将结果的维数减少到300维，并且将术语和上下文对称地组合到单个词嵌入矩阵中。  
这给出了一个词嵌入矩阵，我们称之为ConceptNet-PPMI。这些嵌入隐式表示ConceptNet的整体图结构，并允许我们计算任意一对节点的近似连通性。  
我们可以扩充ConceptNet-PPMI来还原我们修剪掉的节点，指派其向量为其相邻节点的平均值。  
## 将ConceptNet与分布词嵌入相结合
仅从ConceptNet创建嵌入后，我们现在想创建一组更健壮的嵌入，以表示ConceptNet和从文本中学到的分布词嵌入。  
翻新（Faruqui et al.2015）是使用知识图谱（嵌入）调整现有词嵌入矩阵的过程。翻新通过最小化目标函数，推导出新的向量  
Faruqui等人给出一个简单的迭代过程，在原始嵌入的词汇表上最小化该目标函数。  
“扩充翻新”的过程（Speer和Chin，2016年）可以在更大的词汇表中优化该目标，包括来自知识图谱但未出现在词嵌入的词汇表中的术语。
扩充翻新ConceptNet的特别好处是，它可以受益于ConceptNet中的多语言连接。它通过其他语言的翻译来学习有关英语单词的更多信息，并在与英语单词相同的空间中为其他语言术语提供有用的嵌入。效果类似于Xiao和Guo（2014）的工作，他们还使用众包的Wiktionary条目传播多语言嵌入。  
我们在翻新中又增加了一个步骤，即减去所有翻新产生的向量的均值，然后将其重新归一化为单位向量。翻新有将所有向量移近诸如“person”之类的高度关联的术语的向量的趋势。减去均值有助于确保术语彼此可区分。  
## 组合多个嵌入源
可以将改进应用于任何现有的词嵌入矩阵，而无需访问训练它们的数据。这是特别有用的，因为它可以建立在公开发布的嵌入矩阵上，即便其输入数据不可用或难以获取。  
如“相关工作”部分所述，word2vec和GloVe都提供预训练矩阵。这些矩阵代表了文本的不同领域，并且具有互补的优势，而我们可以从它们中获得最大收益的方式就是将它们一起作为输入。  
为此，我们对这两个矩阵进行了翻新，然后找到一个全局线性投影，该投影将结果与它们的共同词汇对齐。这个过程的灵感来自Zhao, Hassan, and Auli (2015)  。我们通过连接（concatenate）矩阵的列并使用截断SVD将它们缩小为300维来找到投影。然后，我们使用此对齐来推导出某个词汇表中缺少的术语的嵌入。  
在正在进行的工作中，我们正在尝试在此合并中另外包括非英语文本语料库的分布词嵌入。初步结果表明，这提高了嵌入的多语言性能。  
经过翻新和合并后，我们得到了一个词嵌入的带标签矩阵，其词汇表是从word2vec，GloVe和修剪的ConceptNet图获得的。像在ConceptNet-PPMI中一样，我们通过查找并计算相邻节点的平均值来重新引入ConceptNet中的所有节点。  

