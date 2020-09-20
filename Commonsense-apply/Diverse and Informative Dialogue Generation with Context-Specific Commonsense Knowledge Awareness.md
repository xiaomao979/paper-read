# 论文目的
生成对话系统总会产生无意义的对话，例如“我不知道”，所以本论文利用常识来补充对话背景信息，为对话增添色彩
# 论文方法
Knowledge fact set F is retrieved by the Knowledge Retriever given the query message X. The Context Encoder summarizes an utterance into contextual representations. The Felicitous Fact Recognizer calculates the felicitous
fact probability distribution z over the F, which is used to initialize the Decoder and guide the generation. The Triple Knowledge Decoder can generate three types of words: vocabulary words, entity
words, and copied words, with the Flexible Mode Fusion.

# 实验方法
## baseline
For the compared methods, we select models and classify them into 4 groups.   
Group 1: models without descriptions or papers,   
Group 2: models without extracted knowledge,  
Group 3: models with extracted structured knowledge and  
Group 4: models with extracted unstructured knowledge.  

## 实验内容
1. 在CommonsenseQA上对比baseline效果
2. Ablation Study——对比模型简化版本以证明每个模块的有效性
3. case study
4. 误差分析——the lack of evidence, similar evidence and dataset noise


# 论文亮点
实验做得极其充分
