# Background:
KG中数据的主要形式为(head,relation,tail)  
针对结构化的数据：传统机器学习的方法的关注点主要是在基于特征的表示上面。  
KG completion – 基于KG中现有的三元组，推出新的三元组。  
在关系学习中，embedding主要通过张量分解的形式实现，需要依赖于大量的标注三元组。而在知识库中存在着一些taxonomy的信息，如子类和子属性，比如知识库中有（DJ Trump  isA  president），但可能没有（DJ Trump  isA  person）,但这个信息是隐含在taxonomic knowledge里面的，再比如being president 是managing的子属性，managing是“interacts with”的子属性等。

# 本文贡献
这篇文章的主要贡献是将taxonomy中的子类和子属性信息整合到了embedding model中。  
首先论证了现有的模型的局限性，没有体现以上的taxonomic information,提出了一个新模型，SimpIE+，然后通过实验证明了他们的模型不仅是fully expressive 并且能够反映taxonomic information
