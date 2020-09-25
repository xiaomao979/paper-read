# 论文目的
通过捕获图像当中的常识来解决VQA（Visual Question Answering）和captioning（给图片加说明文字）

# 论文方法
使用R-CNN结合causal intervention
## causal intervention
通过将干预P(Y | do(X))作为特征学习目标，我们可以在 “common” and “sense-making”之间进行调整，从而减轻观察偏差

通过构建一个字典来把广泛存在于其他图片中的物体“borrow”到当前图片中。

然后把借来的物体“put”到X、Y周围和X、Y对比，例如上图中的把 sink、handbag、chair等等移到 toilet和person 周围，然后通过后门调整公式计算干预后的值。

最后通过一种自监督学习的方式学习到图片局部物体的更好的表征——我们称之为视觉常识特征

