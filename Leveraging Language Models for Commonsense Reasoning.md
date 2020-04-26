# 论文目的
对常识问答. Common sense Question Answering (CQA) 中的答案进行自动化解释Commonsense Auto-Generated Explanations (CAGE)
# 论文理论
人工标注解释——Human participants对问题进行回答，并对回答进行解释，由此构建训练集  
模型形式——一个问题q，三个回答选项c1,c2,c3，一个正确答案a,一个人类解释eh,输出的是与eh尽可能相近的机器解释e  
## 模型使用  
Bert模型——将问题和解释放在一起，将答案放在另一端（For BERT, the explanations share the same input representation as that of the questions）  
CAGE-reasoning模型——将问题、答案和解释放到一起作为信息，最大化条件概率求解释信息
C_RE = “q, c0, c1, or c2?commonsense says ” 最大化\sum log P(ei|ei-k, . . . , ei-1, C_RE; Θ)
# 实验方法
把bert模型与CAGE-reasoning比较
