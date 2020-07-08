# 摘要
经过大量原始文本数据训练的上下文表示法已经对NLP任务（包括问题回答和阅读理解）进行了显着改进。已经有工作表明语法，语义和词义知识包含在此类表示中，这解释了它们为何有益于此类任务。但是，有关情境化表示中所包含的常识知识的研究工作相对较少，这对于人类对问题的回答和阅读理解至关重要。我们通过在七个具有挑战性的基准测试中测试了GPT，BERT，XLNet和RoBERTa的常识能力，发现语言建模及其变体是提升模型常识能力的有效目标，而双向上下文和更大的训练集则是加分项。我们还发现，当前的模型无法很好地完成任务，需要更多必要的推理步骤。最后，我们通过制作双重测试用例来测试模型的健壮性，这些用例相互关联，这样一个样本的正确预测应该导致另一个样本的正确预测。有趣的是，这些模型在这些测试用例上显示出混乱，这表明它们在表面而不是深层学习常识。我们发布了一个测试集，公开称为CAT，以供将来研究。
# 论文目的
用五种[GPT (Radford and Sutskever 2018), GPT2 (Radford et al.2019), BERT (Devlin et al. 2019), XLNet (Yang et al. 2019) and RoBERTa (Liu et al. 2019b)]最先进的模型来评估七种[ Conjunction Acceptability, Sense Making (Wang et al.2019), Winograd Schema Challenge (Levesque, Davis, and Morgenstern 2012), SWAG (Zellers et al. 2018), HellaSwag (Zellers et al. 2019), Sense Making with Reasoning (Wang et al. 2019), and Argument Reasoning Comprehension (Habernal et al. 2018).]常识基准.

# 七种常识基准
## Sense Making (SM)
由Wang等人介绍。 （2019），该任务测试模型是否可以区分有意义的陈述和无意义的陈述。 给定一对语句（即测试实例），它需要模型选择更明智的语句。 一个例子是：我一天工作8小时/我一天工作25小时。 该任务无需更改就符合我们的评估架构。 语句通常仅在一个关键词上有所不同，该关键词涵盖名词，动词，形容词和副词。
- money can be used for buying cars （correct）
- money can be used for buying stars（wrong）

## Winograd Schema Challenge (WSC)
Winograd Schema Challenge（WSC）数据集（Levesque，Davis和Morgenstern 2012）包含273个代词解决问题实例。 每个实例包含一个带有代词的句子，代词指代一个名词。 最初的问题是选择正确的名词。 对于我们的任务，我们将转换测试，WSC被认为是最困难的常识数据集之一
- The trophy doesn’t fit into the brown suitcase because the trophy is too large. （correct）
- The trophy doesn’t fit into the brown suitcase because the suitcase is too large（wrong）

## Conjunction Acceptability (CA)
如LoBue和Yates（2011）所述，基于逻辑的常识知识除基于内容的知识外，还是世界知识的重要组成部分。我们的目的是通过从WSC数据集中提取189个阳性样本，并用另一种人工替换连接词以获得阴性样本，从而探索模型理解语言中逻辑关系的能力。我们将正负样本配对以获得测试实例。此任务使用“因为”，“之前”，“何时”，“但是”，“和”来对应因果，先决条件，同时条件，矛盾和附加逻辑关系分别。
- They broadcast an announcement, but a subway came into the station and I couldn’t hear it. （correct）
- They broadcast an announcement, before a subway came into the station and I couldn’t hear it .（wrong）

## SWAG
它质疑模型对两个物理场景之间关系的理解
- Someone unlocks the door and they go in. → Someone leads the way in. （correct）
- Someone unlocks the door and they go in. → Someone opens the door and walks out. （wrong）
- Someone unlocks the door and they go in. → Someone walks out of the driveway. （wrong）
- Someone unlocks the door and they go in. → Someone walks next to someone and sits on a pew. （wrong）

## HellaSwag
HellaSwag（Zellers et al.2019）是SWAG的有争议版本，具有与SWAG相同的数据格式，更多的推理步骤和更高的数据质量。 尽管HellaSwag还包括WikiHow的数据集，但我们仅选择来自ActivityNet的实例，以使结果与原始SWAG数据集可比。  
 A carved pumpkin with a light in it glows on a counter. Supplies for carving are then shown.
- A woman cuts the top off the pumpkin, emptying the seeds. （correct） 
- she cuts down all the pieces and dumps them in a trash bin in the end. （wrong）
- she then carves the traced lines to cut out the design. （wrong）
- she tapes the top shut as the continue carving the pumpkin.（wrong）

## Sense Making with Reasoning (SMR)
理性推理使人专注于确定针对常识的陈述（Wang等，2019）背后的原因。 模型需要了解特定的陈述是否违背常识，并且要从三个候选者中做出背后原因的选择。 通过将陈述和候选原因串联在一起，可以得出正面或负面的样本。 对于SMR中的每个测试实例，有一个正样本和两个负样本。 此任务在直观上很困难，因为它要求模型具有更高层次的推理知识，这属于归纳推理。
- “ he put an elephant into the fridge” (because) ← an elephant is much bigger than a fridge . （correct） 
- “ he put an elephant into the fridge ” (because) ← elephants are usually gray.（wrong）  
- “ he put an elephant into the fridge ” (because) ← an elephant cannot eat a fridge . （wrong）

## Argument Reasoning Comprehension Task(ARCT)
它的领域在于社交主题，例如搜索引擎和LGBT权利
- People can choose not to use Google and Other search engines dont redirect to Google -> Google is not a harmful monopoly （correct） 
- People can choose not to use Google and All other search engines redirect to Google -> Google is not a harmful monopoly（wrong） 
# 论文方法
1. 数据集构建通过正负样本采样
2. 为了检测模型的鲁棒性，作者将测试集中的个别单词进行编辑（删除/替换/增加），得到与原测试集相近的错误的测试集

# 论文结论
从结果来看，我们有四个明显的观察结果。   
1. 预训练的模型始终比随机基准提供更好的性能，这表明语言模型的预训练对于学习常识知识很有用。 
2. 与基于双向上下文（例如GPT和GPT2）的模型相比，基于BERT，XLNet和RoBERTa等双向上下文的模型在学习常识方面更强大。 
3. 可以从较大的训练集中学习更多常识知识，这与直觉很吻合。 
4. 模型具有一定程度的常识推理能力。 但是，随着所需推理步骤数量的增加，模型性能下降，这表明常识仍然是一个巨大的挑战，而预训练的上下文化语言模型（LM）不能完全解决常识
5. 从理论上讲，配备相关常识的模型应在一对双重测试用例上给出一致的预测。 但是，我们发现没有一个模型能够达到这样的一致性。 取而代之的是，模型被修改所迷惑，尽管它们可能具有不同的标签，但它们往往会在一对双重样本上给出相同的预测。 这进一步表明，预训练模型中包含的常识可能会停留在表面层面，而无需深入的语义理解。 我们在GitHub上公开发布了名为常识能力测试（CAT）的数据集和测试脚本


