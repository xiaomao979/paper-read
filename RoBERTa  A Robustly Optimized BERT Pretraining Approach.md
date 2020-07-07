参考：https://www.jianshu.com/p/eddf04ba8545

在XLNet全面超越Bert后没多久，Facebook提出了RoBERTa（a Robustly Optimized BERT Pretraining Approach）。再度在多个任务上达到SOTA。那么它到底改进了什么？它在模型层面没有改变Google的Bert，改变的只是预训练的方法。

# 静态Masking vs 动态Masking
原来Bert对每一个序列随机选择15%的Tokens替换成[MASK]，为了消除与下游任务的不匹配，还对这15%的Tokens进行（1）80%的时间替换成[MASK]；（2）10%的时间不变；（3）10%的时间替换成其他词。但整个训练过程，这15%的Tokens一旦被选择就不再改变，也就是说从一开始随机选择了这15%的Tokens，之后的N个epoch里都不再改变了。这就叫做静态Masking。
而RoBERTa一开始把预训练的数据复制10份，每一份都随机选择15%的Tokens进行Masking，也就是说，同样的一句话有10种不同的mask方式。然后每份数据都训练N/10个epoch。这就相当于在这N个epoch的训练中，每个序列的被mask的tokens是会变化的。这就叫做动态Masking。
那么这样改变是否真的有效果？作者在只将静态Masking改成动态Masking，其他参数不变的情况下做了实验，动态Masking确实能提高性能。

# with NSP vs without NSP
原本的Bert为了捕捉句子之间的关系，使用了NSP任务进行预训练，就是输入一对句子A和B，判断这两个句子是否是连续的。在训练的数据中，50%的B是A的下一个句子，50%的B是随机抽取的。
而RoBERTa去除了NSP，而是每次输入连续的多个句子，直到最大长度512（可以跨文章）。这种训练方式叫做（FULL - SENTENCES），而原来的Bert每次只输入两个句子。实验表明在MNLI这种推断句子关系的任务上RoBERTa也能有更好性能。

# 更大的mini-batch
原本的BERTbase 的batch size是256，训练1M个steps。RoBERTa的batch size为8k。为什么要用更大的batch size呢？（除了因为他们有钱玩得起外）作者借鉴了在机器翻译中，用更大的batch size配合更大学习率能提升模型优化速率和模型性能的现象，并且也用实验证明了确实Bert还能用更大的batch size。

# 更多的数据，更长时间的训练
借鉴XLNet用了比Bert多10倍的数据，RoBERTa也用了更多的数据。性能确实再次彪升。当然，也需要配合更长时间的训练。


