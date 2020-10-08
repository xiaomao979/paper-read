# 论文目的
将常识融入到看图讲故事当中
# 论文方法
## 任务描述
给定五张有顺序的图片，产生五个句子组成的合理连贯的故事。
## Method
- Vision-Aware Commonsense Reasoning：对于输入的图像流，模块R首先推断出每张图片的关键概念，并对关键概念进行图谱查询获取邻居信息构成子图谱。随后利用self-attention，获取得到与当前图片最为相关的概念信息。
- Knowledge-Augmented Generation：此模块主要是生成故事。当模块产生第i个句子时，可以利用的信息有三个，the semantic representation hvi and commonsense representation hci of the i-th image, and the previously generatedi − 1 sentences that are concatenated into a word sequence gi = (gi1, ··· , gili ).
# 实验内容
## Dataset
我们对VIST数据集进行实验，该数据集包含10117张Flickr相册和210819张独特的照片。 每个样本包含5张图片，每张图片都与故事中的句子配对。
## 实验过程
1. baseline
2. 消融实验
3. case study
4. 展示了模型判断每个概念在每张图片的重要性
