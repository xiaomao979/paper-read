# 摘要
Winograd模式挑战既是常识推理又是对自然语言理解的挑战，是图灵测试的替代方法。 Winograd模式是一对句子，它们在一个或两个单词中具有高度歧义的代词，在两个句子中以不同的方式解析，这似乎要求常识才能正确解析。 这些示例的设计目的是易于人为解决，但对于机器而言则很困难，原则上需要深入理解本文的内容及其所描述的情况。 本文回顾了自引入以来已发布的现有Winograd Schema Challenge基准测试数据集和方法。

# Introduction
Hector Levesque [Levesque et al。，2012]引入了Winograd Schema Challenge，既是Turing测试[Turing，1950]的替代方案，又是对系统进行常识推理能力的测试。Winograd schema的一个例子是 Terry Winograd[1972]引入的一对句子：  
- 市议员拒绝示威者因为他们[害怕/提倡]暴力而获得许可。The city councilmen refused the demonstrators a permit because they [feared/advocated] violence
- 问题：谁[害怕/主张]暴力？Who [feared/advocated] violence?
- 答案：市议员/示威者 the city councilmen / the demonstrators
这个they是指市议员或示威者，具体取决于句子中使用的是恐惧还是鼓吹。为了正确识别目标对象，人们可能需要了解很多有关示威者，许可证，市议员和示威活动的知识。   
Levesque的见解是，人们可以构建许多其他的句子对，这些句子似乎依赖于常识推理，并且句子结构无助于消除歧义。 他声称，在解决此类句子时可以实现人类表现的系统将具有人类在进行此类歧义消除时所使用的常识。 这样的句子对必须被构造为具有某些特性，包括除了一个或两个“特殊”单词以外，它们是相同的，并且不能通过‘选择限制’来解决。一个重要的约束条件是Winograd模式是“ Google验证”的或非关联的[Trichelair等，2018]，这意味着不能使用统计关联来消除代词的歧义。正如我们下面讨论的那样，这是最不可能实现的约束，如调查中描述的统计语言模型的成功所表明的那样。 Winograd Schema挑战之所以吸引人，是因为对人类而言，代词歧义消除的任务是简单而自动的，评估指标很明确，并且使用双句的技巧似乎消除了使用结构化技术来以正确的方式获得正确答案的技巧。避免使用常识性推理。在其发布后的几年中，挑战成为常识推理和自然语言处理社区的研究重点。去年取得了很大进展。在本文中，我们回顾了测试本身的性质，其不同的基准数据集以及用于解决这些问题的不同技术。

# Winograd Schema Challenge Datasets
Several Winograd Schema Challenge datasets have been introduced; for the most part, they can be split into two categories: performance-measuring and diagnostic datasets.

## Original Collection of Winograd Schemas
首先发布了100个Winograd模式的集合，并引入了Winograd模式挑战[Levesque et al。，2012] 1。 AI专家手动构建了示例，并提供了每个示例的确切来源。在撰写本文时，有285个示例可用。但是，仅在最近才添加了最后12个示例。为了确保与早期模型的一致性，一些作者通常更喜欢仅报告第一个273个示例的性能。这些数据集通常分别称为WSC285和WSC273。    
Subclasses of the original collection（原始集合的子类）已观察到WSC273数据集中的37个句子（占13.6％）在概念上比其余句子更容易。正确的候选项通常与句子的其余部分相关联，而错误的候选项则不相关。例如，  
- 在暴风雨中，那棵树倒下并从我家的屋顶坠毁。现在，我必须将它[修复/移除]。  
屋顶通常与被修复相关，而树木则与之无关。他们将这些示例称为关联（associative）的，并将其余示例命名为非关联的。而且，他们发现模型通常在关联子集上表现更好。  
此外，如果切换句子中的候选项，则会发现131个句子（占WSC273的48％）构成有意义的示例。
- 鲍勃倒在人行道上就是这样一个例子。很快，他看到卡尔来帮忙。他非常[病/担心]。  
在这句话中，鲍勃和卡尔可以互换以获得具有相反答案的等效示例。这样的句子被命名为可切换的（switchable）。 Trichelair等鼓励未来的研究人员另外报告可切换数据集的一致性，何时切换候选者以及何时不切换候选者。关联和可切换示例的列表以及与之对应的示例已公开。  
Winograd Schema Challenge in other languages（Winograd Schema Challenge用其他语言）。 挑战的灵感和原始设计是英语，但存在其他语言的翻译。 Amsili和Seminck [2017]将144个Winograd模式的集合翻译成法语，Melo等人将285个原始Winograd模式翻译成葡萄牙语。 [2020]。 此外，可以在挑战赛的官方网页上获得Japanese3和Chinese4的翻译。 法语和葡萄牙语翻译的作者均报告说，必须对内容进行一些更改，以避免出现意想不到的暗示，例如语法性别。 就葡萄牙语而言，由于找不到适当的翻译，因此不得不删除8个句子。  
##  Definite Pronoun Resolution Dataset
限定代词解析度（DPR）数据集是Winograd Schema Challenge [Rahman and Ng，2012]的较简单变体。对Winograd模式的约束已经放松，并且数据集中的一些示例不是Google可靠的。该数据集包含1322个训练示例和564个测试示例，它们是手动构建的。训练集中的6个示例以非常相似的形式出现在WSC273中。在进行DPR培训并在WSC273上进行评估时，应删除这些内容。这个数据集也被称为WSCR，由Opitz和Frank [2018]命名。 Peng等人已经发布了该数据集的扩展版本，称为WINOCOREF。 [2015]，他进一步注释了原工作中未注释的句子中以前忽略的所有提及（在他们的工作中，提及可以是代词或实体）。这样，他们将746个提及添加到数据集中，其中709个是代词。此外，彭等。 [2015]认为准确性不是WINOCOREF数据集上适当的性能指标，并引入了一个新的称为AntePre的数据。他们对AntePre的定义如下：假设数据集中有k个代词，每个代词都有n1 ，。 。 。 ，nk个先例。我们可以将为每个代词找到正确的候选者作为对每个先行代词对的二元分类。令m为正确的二元决策数。然后将AntePre计算为m / sum（n）
##  Pronoun Disambiguation Problem Dataset
代词歧义消除问题（PDP）数据集由从经典和大众文学，报纸和杂志中收集的122个代词歧义消除问题组成。由于根据Levesque的原始指南构建Winograd模式是一个困难的手动过程，因此，在管理Winograd Schema Challenge之前，将收集并审查而不是构建的PDP用作网关集[Morgenstern等，2016 ]。每个PDP收集后都会经过审核（有时会进行修改），以确保像Winograd模式一样，问题属于人类使用常识来消除歧义的问题，并且是“ Google验证”的问题。尽管对每个PDP进行了审查，都删除了一些句子结构有助于查找答案的示例，但由于没有“特殊”单词，因此与Winograd模式不同，不能保证不能利用句子结构。因此，人们希望PDP比Winograd模式更容易。示例：  
- 您认为彼得是船长生病的原因吗？也许他贿赂厨师在他的食物中放些东西。  
- 他的指称者是：（a）彼得或（b）队长。  
在进行Winograd Schema Challenge 5之前已发布了62个PDP实例，在IJCAI 2016 6进行的Winograd Schema Challenge中包含了60个PDP [Davis et al。，2017]。 Davis和Pan [2015] 7从在线文本中半自动收集了400个句子的语料库，其审查较少。
## Winograd Natural Language Inference Dataset
