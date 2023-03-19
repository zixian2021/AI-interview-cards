# Transformer

# 初级:

Q1：***Transformer为何使用多头注意力机制？***

- 多头保证了transformer可以注意到不同子空间的信息，捕捉到更加丰富的特征信息。可以类比CNN中同时使用多个通道的作用，直观上讲，多头的注意力有助于网络捕捉到更丰富的特征/信息。

Q2：***Transformer的self attention为什么Q和K使用不同的权重矩阵生成，为何不能使用同一个值进行自身的点乘？***

- 使用不同的权重矩阵生成QKV可以保证word embedding在不同空间进行投影，增强了表达能力，提高了泛化能力

Q3：**Self-attention计算时为什么在进行softmax之前需要除以dk的平方根**

- Self-attention计算时为什么在进行softmax之前需要除以dk的平方根（对梯度进行scale，缓解梯度消失的问题，dk的平方根为根据经验选择的参数）

Q4：***transformer的并行化体现在哪里？***

- 在encoder和decoder的训练阶段可以并行训练（通过teacher-forcing和sequence mask），但在transformer推理时无法并行，需要单步自回归推理，类似于RNN）

Q5：***transformer在音视频领域落地时需要注意的问题***

- 由于attention计算需要全局信息，会造成系统的高延时以及巨大的存储开销，需要设计chunk-wise attention，做流式解码

Q6：***transformer中的mask机制***

- transformer中包含padding mask与sequence mask，前者的目的是让padding(不够长补0)的部分不参与attention操作，后者的目的是保证decoder生成当前词语的概率分布时，只看到过去的信息，不看到未来的信息（保证训练与测试时的一致性）

Q7：***Transformer为什么Q和K使用不同的权重矩阵生成，为何不能使用同一个值进行自身的点乘？***

- 使用Q/K/V不相同可以保证在不同空间进行投影，增强了表达能力，提高了泛化能力。
- 同时，由softmax函数的性质决定，实质做的是一个soft版本的arg max操作，得到的向量接近一个one-hot向量（接近程度根据这组数的数量级有所不同）。如果令Q=K，那么得到的模型大概率会得到一个类似单位矩阵的attention矩阵，这样self-attention就退化成一个point-wise线性映射。这样至少是违反了设计的初衷。

Q8：***Transformer计算attention的时候为何选择点乘而不是加法？两者计算复杂度和效果上有什么区别？***

- K和Q的点乘是为了得到一个attention score 矩阵，用来对V进行提纯。K和Q使用了不同的W_k, W_Q来计算，可以理解为是在不同空间上的投影。正因为 有了这种不同空间的投影，增加了表达能力，这样计算得到的attention score矩阵的泛化能力更高。
- 为了计算更快。矩阵加法在加法这一块的计算量确实简单，但是作为一个整体计算attention的时候相当于一个隐层，整体计算量和点积相似。在效果上来说，从实验分析，两者的效果和dk相关，dk越大，加法的效果越显著。

# 中级:

Q9：***为什么在进行多头注意力的时候需要对每个head进行降维？***

Q10：***简单介绍一下Transformer的位置编码？有什么意义和优缺点？***

Q11：***为什么transformer使用LayerNorm而不是BatchNorm？LayerNorm 在Transformer的位置是哪里？***

Q12：***简答讲一下BatchNorm技术，以及它的优缺点***

Q14：***Transformer中，Encoder端和Decoder端是如何进行交互的？***

Q15：**Transformer中，*Decoder阶段的多头自注意力和encoder的多头自注意力有什么区别？***

Q16：***Bert的mask为何不学习transformer在attention处进行屏蔽score（sequence mask）的技巧？***

Q17：***简单讲述一下wordpiece model 和BPE（byte pair encoding）方法***

Q18：***解释self- attention，它与其他attention的异同？***

Q19：****Transformer 相比于 RNN/LSTM，有什么优势？为什么？****

# 高级:

Q20：***除了绝对位置编码技术之外，还有哪些位置编码技术？***

Q21：*****在 BERT 中，token 分 哪3 种情况 mask，分别的作用是什么？*****

Q22：*****elmo、GPT、bert三者之间有什么区别？*****

Q23：***简述BERT模型的优缺点***

Q24：***简述Label Smoothing及其作用***

Q25：****BERT训练时使用的学习率 warm-up 策略是怎样的？为什么要这么做?****
