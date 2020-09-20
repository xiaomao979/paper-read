借鉴博文：https://zhuanlan.zhihu.com/p/109886447  
# 论文目的
对常识问答. Common sense Question Answering (CQA) 中的答案进行自动化解释Commonsense Auto-Generated Explanations (CAGE)

常识推理任务CQA(Commonsense Question Answer)是机器阅读理解中更具挑战性的任务，它的输入包括one question, one correct answer, serveral distraction answers，要求输出correct answer。CQA任务的挑战性来源缺乏commonsense knowledge用于推理出正确答案，作者提出了一个Commonsense Auto-Generated Explanations (CAGE)的框架，是利用预训练语言模型生成explanation，为CQA任务加入commonsense knowledge信息。
# 论文理论

文章实验所用的数据库  
CQA dataset：常识推理数据库：一个问题，五个答案，其中一个正确答案四个干扰答案，需要利用常识预测答案  
Cos-E dataset：针对CQA dataset中的每个sample，附加上human explanation，human explanation有两种形式  
(1)问题描述中的highlighted text span  
(2)open-ended的解释，人类语言给出的解释  

人工标注解释——Human participants对问题进行回答，并对回答进行解释，由此构建训练集  
模型形式——一个问题q，三个回答选项c1,c2,c3，一个正确答案a,一个人类解释eh,输出的是与eh尽可能相近的机器解释e  
## 模型使用  
Bert模型——将问题和解释放在一起，将答案放在另一端（For BERT, the explanations share the same input representation as that of the questions）  
CAGE-reasoning模型——将问题、答案和解释放到一起作为信息，最大化条件概率求解释信息
C_RE = “q, c0, c1, or c2?commonsense says ” 最大化\sum log P(ei|ei-k, . . . , ei-1, C_RE; Θ)
# 实验方法
把bert模型与CAGE-reasoning、Cos-E-open比较
Cos-E-open与CAGE-reasoning方法中的分类模型都是Bert模型，该Bert模型直接以CQA dataset训练得到。区别是Cos-E-open中explanation为human explanation，CAGE-reasoning中explanation为GPT生成的explanation。  
用不同生成方法生成的解释，加入到CQA任务的输入中，用同一个Bert模型进行分类对比效果，目的是去对比生成解释方法的性能，可以看到CAGE-reasoning方法比单纯的GPT方法提升了接近十个百分点。  

