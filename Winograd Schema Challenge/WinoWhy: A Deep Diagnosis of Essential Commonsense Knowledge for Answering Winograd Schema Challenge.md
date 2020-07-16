# 摘要
在本文中，我们提出了基本常识知识的第一个综合分类，用于回答Winograd模式挑战（WSC）。对于每个问题，我们邀请注释者首先提供做出正确决定的原因，然后将其归类为六个主要知识类别。这样一来，我们可以更好地理解现有方法的局限性（即无法用现有方法有效地表示或推论哪种知识），并为将来为更好的常识推理而需要获取的常识提供一些启示。此外，为了调查当前的WSC模型是否可以理解常识，或者仅基于数据集的统计偏差来解决WSC问题，我们利用收集到的原因开发了一个名为WinoWhy的新任务，该任务需要模型将可能的原因与非常明显的原因区分开来。所有WSC问题的相似但错误的原因。实验结果证明，即使在原始WSC数据集上经过预训练的语言表示模型取得了可喜的进展，但它们仍在WinoWhy上苦苦挣扎。进一步的实验表明，尽管监督模型可以实现更好的性能，但是这些模型的性能可能对数据集的分布很敏感。 WinoWhy和所有代码都可以在以下网址获得： https://github.com/HKUST-KnowComp/WinoWhy

# 论文目的
为了了解针对Winograd模式挑战的模型为什么好（can these models understand commonsense or they just capture the statistical bias of the dataset），作者对回答WSC问题的基本常识进行首次深度诊断，即让受试者回答做出选择的原因。基于这些原因，可以将WSC分为不同的类型，我们可以看看模型在哪个类做的好，哪个类做的不好。并且提出了WinoWhy数据集

# 论文方法
## Reason Collection
在Amazon Mechanical Turk (MTurk)平台上，设计两个阶段
1. 让受试者回答WSC做出选择的原因（每五个人回答一个问题，确保收集到足够全面的原因）
2. 让受试者判断原因的合理性（每五个人判断一个问题，确保判断足够准确）

## Knowledge Categorization

| Name | Definition |  Example |
|  ----  | ----  | ----  | 
| Property | Knowledge about property of objects. | ice is cold. |
| Object | Knowledge about objects. | cats have ears.|
| Eventuality | Knowledge about eventualities. | ‘wake up’ happens before ‘open eyes’.|
| Spatial | Knowledge about spatial position.| object at the back can be blocked. |
| Quantity | Knowledge about numbers. | 2 is smaller than 10. | 
| Others | All other knowledge. | NA | 

## WinoWhy

# 论文结论
通过实验可以得出，尽管当前的模型在WSC挑战上以及达到了90%的准确率，但是在WinoWhy数据集上的效果非常不好，这说明当前的模型还是离理解常识差的很远。
