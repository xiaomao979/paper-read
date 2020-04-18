# 论文目的
在缺少上下文的前提下，通过数据库中已存在的符合事实的三元组的信息，判断一个新的三元组是否符合事实（we are provided with a large database of facts 
which we believe to be true, and a query fact not in the database. The task is to output a judgment on whether the fact is 
plausible (true unless we have reason to believe otherwise), with an associated confidence）

# 论文理论
## 具体路线
发现数据库中与查询三元组相似的信息（可能是多个三元组，可能的单个三元组），并计算相似度，最后将相似度汇总得到置信度。（(i) we find candidate facts
that are similar to our query, (ii) we define a notion of similarity between these facts and our query,
and (iii) we define a method for aggregating a collection of these similarity values into a single judgment.）

## word similarity
数据库中与查询三元组相似的信息很少，如同大海捞针；如果候选集增多，那么误差就会变大。所以如何快速并获取较为准确的候选集就需要多方考量。
论文当中最苛刻解决的办法就是通过规定至少精确匹配两项，才可以加入到候选集当中，但这样就会导致候选集太小了，举个例子  
查询三元组——(private land, be sold to, government)，(his land, be sold to, United States)其实是一个很好的选择，但是因为只是精确匹配了一项，
所以就不会把它放到候选集当中

然后文章中提出了三种选取候选集的方法，  

第一种是通过匹配短语中第一个word即可，第二种是匹配短语中的动词/名词即可，第三种是匹配短语中的形容词即可。

## 计算相似度
Thesaurus Based和Distributional方法计算相似度。首先将三元组编译为词向量，对于短语，是将每个单词的词向量求出来取平均（Compound phrases are queried by treating the
phrase as a bag of words and averaging the word vectors of each word in the phrase, pruning out unknown words.）

## 汇总相似度
分为两个维度的汇总，第一个维度是汇总单个相似性矩阵，第二个维度是汇总这些汇总后的aggregate judgements.也就是说一共11种计算相似度的方法，我们都计算一边，然后汇总这些相似度值
### 第一维度汇总——Thresholded Average Similarity
对于单个相似度矩阵，取前百分之五的相似度值后取平均

### 第二维度汇总——Aggregate Similarity Values
对于每种方法计算的值，做逻辑回归。

# 实验方法
使用ReVerb和ConceptNet数据库，负样本是替换常识三元组中的一个实体或关系
