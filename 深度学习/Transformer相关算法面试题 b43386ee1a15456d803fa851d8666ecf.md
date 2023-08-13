# Transformer相关算法面试题

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

Q9：***为什么在进行多头注意力的时候需要对每个head进行降维？***

- 将原有的高维空间转化为多个低维空间并再最后进行拼接，形成同样维度的输出，借此丰富特性信息

Q10：***简单介绍一下Transformer的位置编码？有什么意义和优缺点？***

- 因为self-attention是位置无关的，无论句子的顺序是什么样的，通过self-attention计算的token的hidden embedding都是一样的，这显然不符合人类的思维。因此要有一个办法能够在模型中表达出一个token的位置信息，transformer使用了固定的positional encoding来表示token在句子中的绝对位置信息。

Q11：***为什么transformer使用LayerNorm而不是BatchNorm？LayerNorm 在Transformer的位置是哪里？***

- Layernorm在特征维度上做归一化，Batchnorm在样本维度做归一化。使用layernorm的原因是transformer的处理文本序列通常是变长序列，batch内数据分布有很大差异，对样本维度做归一化意义不大，相比较之下，对每个序列自身特征做归一化的layernorm更稳定
- Layernorm在多头注意力层和激活函数层之间

引用：[https://zhuanlan.zhihu.com/p/363466672](https://zhuanlan.zhihu.com/p/363466672)

Q12：***简答讲一下BatchNorm技术，以及它的优缺点***

- BN批归一化是对每一批的数据在进入激活函数前进行归一化，可以提高收敛速度，防止过拟合，防止梯度消失，增加网络对数据的敏感度

Q14：***Transformer中，Encoder端和Decoder端是如何进行交互的？***

- 通过encoder-decoder端的attention，Encoder的输出作为K，V，Q来自decoder

Q15：**Transformer中，*Decoder阶段的多头自注意力和encoder的多头自注意力有什么区别？***

- Decoder有两层mha，encoder有一层mha，Decoder的第二层mha是为了转化输入与输出句长，Decoder的q、k和v的倒数第二个维度可以不一样，但是encoder的qkv维度一样。
- Decoder的attention加入了sequence mask，让模型无法看到将来的信息，保证整体系统的因果性

Q16：***Bert的mask为何不学习transformer在attention处进行屏蔽score（sequence mask）的技巧？***

- BERT和transformer的目标不一致，bert是语言的预训练模型，需要充分考虑上下文的关系，而transformer需要保证其因果性，主要考虑句子中第i个元素与前i-1个元素的关系。

Q17：***简单讲述一下wordpiece model 和BPE（byte pair encoding）方法***

- 在NLP领域传统的分词方法是使用空格分词得到固定的词汇，带来的问题是遇到罕见的词汇无法处理即OOV（Out of Vocabulary）问题；同时传统的分词方法也不利于模型学习词缀之间的关系或词的不同时态之间的关系。比如：walked, walking，walker之间的关系无法泛化到talked，talking，talker，word piece和BPE都属于子词方法，解决上述问题
- Byte Pair Encoding字节对编码，一种数据压缩方法，将词拆分为子词，具体为将字符串里最常见的一对连续数据字节被替换为该数据中未出现的字节，把词的本身的意思和时态分开
- WordPiece算法可以看作是BPE的变种。不同点在于，WordPiece基于概率生成新的subword而不是下一最高频字节对

引用：[https://medium.com/towards-data-science/byte-pair-encoding-subword-based-tokenization-algorithm-77828a70bee0](https://medium.com/towards-data-science/byte-pair-encoding-subword-based-tokenization-algorithm-77828a70bee0)

Q18：***解释self- attention，它与其他attention的异同？***

- self-attention 可以看成一般 attention 的一种特殊情况。在 self-attention 中，序列中的每个单词(token)和该序列中其余单词(token)进行 attention 计算，具体到计算上即QKV矩阵均源于同源输入。self-attention 的特点在于**「无视词(token)之间的距离直接计算依赖关系，从而能够学习到序列的内部结构」**

Q19：****Transformer 相比于 RNN/LSTM，有什么优势？为什么？****

- RNN 系列的模型，并行计算能力很差；RNN当前时刻的计算依赖于上一个时刻的隐层计算结果，导致RNN的训练无法并行；而Transformer在训练阶段，通过sequence mask掩蔽和teacher-forcing，可以做到并行训练
- 通过一些主流的实验证明，Transformer 的特征抽取能力比 RNN 系列的模型要好

Q20：***除了绝对位置编码技术之外，还有哪些位置编码技术？***

- **相对位置编码**（RPE）技术，具体又分三种：1.在计算attention score和weighted value时各加入一个可训练的表示相对位置的参数。2.在生成多头注意力时，把对key来说将绝对位置转换为相对query的位置3.复数域函数，已知一个词在某个位置的词向量表示，可以计算出它在任何位置的词向量表示。前两个方法是词向量+位置编码，属于亡羊补牢，复数域是生成词向量的时候即生成对应的位置信息。
- ****学习位置编码，****学习位置编码跟生成词向量的方法相似，对应每一个位置学得一个独立的向量

Q21：*****在 BERT 中，token 分 哪3 种情况 mask，分别的作用是什么？*****

- 在 BERT 的 Masked LM 训练任务中， 会用 [MASK] token 去替换语料中 15% 的词，然后在最后一层预测。但是下游任务中不会出现 [MASK] token，导致预训练和 fine-tune 出现了不一致，为了减弱不一致性给模型带来的影响，在这被替换的 15% 语料中：80% 的 tokens 会被替换为 [MASK] token，10% 的 tokens 会称替换为随机的 token，10% 的 tokens 会保持不变但需要被预测
- 第一种替换，是 Masked LM 中的主要部分，可以在不泄露 label 的情况下融合真双向语义信息；
- 第二种随机替换，因为需要在最后一层随机替换的这个 token 位去预测它真实的词，而模型并不知道这个 token 位是被随机替换的，就迫使模型尽量在每一个词上都学习到一个 全局语境下的表征，因而也能够让 BERT 获得更好的语境相关的词向量（这正是解决一词多义的最重要特性）；
- 第三种的保持不变，也就是真的有 10% 的情况下是 泄密的（占所有词的比例为15% * 10% = 1.5%），这样能够给模型一定的 bias ，相当于是额外的奖励，将模型对于词的表征能够拉向词的 真实表征

引用：https://www.jianshu.com/p/55b4de3de410

Q22：*****elmo、GPT、bert三者之间有什么区别？*****

- 特征提取器：elmo采用LSTM进行提取，GPT和bert则采用Transformer进行提取。很多任务表明Transformer特征提取能力强于LSTM，elmo采用1层静态向量+2层LSTM，多层提取能力有限，而GPT和bert中的Transformer可采用多层，并行计算能力强。
- 单/双向语言模型：GPT采用单向语言模型，elmo和bert采用双向语言模型。但是elmo实际上是两个单向语言模型（方向相反）的拼接，这种融合特征的能力比bert一体化融合特征方式弱。
- GPT和bert都采用Transformer，Transformer是encoder-decoder结构，GPT的单向语言模型采用decoder部分，decoder的部分见到的都是不完整的句子；bert的双向语言模型则采用encoder部分，采用了完整句子

Q23：***简述BERT模型的优缺点***

- 优点：并行，解决长时依赖，双向特征表示，特征提取能力强，有效捕获上下文的全局信息，缓解梯度消失的问题等，BERT擅长解决的NLU任务。
- 缺点：生成任务表现不佳：预训练过程和生成过程的不一致，导致在生成任务上效果不佳；
采取独立性假设：没有考虑预测[MASK]之间的相关性，是对语言模型联合概率的有偏估计（不是密度估计）；由于mask引入的输入噪声，造成预训练-精调两阶段之间的差异；无法处理文档级别的NLP任务，只适合于句子和段落级别的任务；

Q24：***简述Label Smoothing及其作用***

- 由于训练集中含有少量错误数据，label smoothing是将正样本的标签修为0.9，负样本的标签修改为0.1（标签平滑的程度可以根据情况修改），这是一种**soft**的学习，也就是告诉模型，**不要这么自信**
- ***Label Smoothing***可以提高神经网络的鲁棒性和泛化能力

Q25：****BERT训练时使用的学习率 warm-up 策略是怎样的？为什么要这么做?****

- warm-up相当于对学习率自适应的一个过程。因为模型一开始参数迭代的方向比较重要，所以在开始训练的时候，避免部分噪声样本把参数更新方向带偏，所以开始训练的时候会设置一个warm-up步数，当前步的学习率和当前步数成正比，即学习率为（current_step/warm_up_step）*learning_rate。