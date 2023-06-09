# CNN

# 初级

Q1：***CNN和RNN有什么区别？什么时候使用它们？***

- CNN最适用于需要平移不变性的情况。平移不变性是指，无论目标出现在图像中的哪个位置，它都会检测到同样的这些特征，输出同样的响应。
- RNN是可以记住历史输入状态信息的神经网络，他们记住历史的输入样本，并使用这些样本来帮助对当前输入样本进行分类。当数据顺序很重要时，适合用RNN。因此，在语音、视频（帧是有序的）以及文本处理中，常常用到RNN。一般来说，与时间序列数据（带有时间戳的数据）相关的问题很适合用RNN解决。

Q2：***CNN怎样被用到时间序列预测中？***

- **CNN**从原始输入数据中学习和自动提取特征的能力可以应用于时间序列预测问题。可以将一系列观察结果视为一维图像，CNN 模型可以读取该图像并提取其中特征，创建时间序列的信息表示
- 常见的将cnn用于时间序列预测的例子包括TCN、wavenet；它们是高度抗噪的模型，并且能够提取信息丰富的深度特征

Q3：***在CNN中，Max Pooling与Average Pooling的优缺点是什么？***

- 卷积层参数误差造成估计均值的偏移，max pooling能减小这种误差；邻域大小受限造成的估计值方差增大，average能减小这种误差。也就是说，average对背景保留更好，max对纹理提取更好。对数字识别等任务，一般使用max-pooling。

引用：[https://www.zhihu.com/question/34898241](https://www.zhihu.com/question/34898241)

Q4：***比较CNN和多层感知机MLP***

- MLP由全连接层构成，每个神经元都和上一层中的**所有**节点连接，存在参数冗余；相比之下，CNN由于权重共享，参数更少，方便网络的训练与设计深层网络；
- MLP只接受向量输入，**会丢失像素间的空间信息；CNN接受矩阵和向量输入，能利用像素间的空间关系**
- MLP是CNN的一个特例，**当CNN卷积核大小与输入大小相同时其计算过程等价于MLP**

引用：[https://medium.com/data-science-bootcamp/multilayer-perceptron-mlp-vs-convolutional-neural-network-in-deep-learning-c890f487a8f1](https://medium.com/data-science-bootcamp/multilayer-perceptron-mlp-vs-convolutional-neural-network-in-deep-learning-c890f487a8f1)

Q*5*： *****CNN*中的*全连接层*有什么作用？**  

- 全连接层在整个网络卷积神经网络中起到“分类器”的作用。如果说卷积层、池化层和激活函数等操作是将原始数据映射到隐层特征空间的话（特征提取+选择的过程），全连接层则起到将学到的特征表示映射到样本的标记空间的作用。换句话说，就是把特征整合到一起（高度提纯特征），方便交给最后的分类器或者回归。

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*Q6*：*****解释RELU激活函数在卷积神经网络中的意义*****

- 在每次卷积操作之后，使用RELU操作。RELU 是一个非线性激活函数。此操作应用于每个像素，并将特征图中的所有负像素值替换为零。卷积操作本身是线性的，为了建模非线性变化的图像特征，需要使用像RELU 这样的非线性函数向模型中引入非线性。

Q7：***对于给定的图像输入尺寸、Filter Size、  Stride 和 Padding大小，feature map 的尺寸是多少？***

- 如果我们的输入图像大小为 nxn，过滤器大小为 fxf，p 是padding size，s 是stride，则特征图的维度为：**floor[ ((n-f+2p)/s)+1] x floor[ ((n-f+2p)/s)+1]**

Q8：***解释Valid Paddding和Same Padding***

- valid padding：**当filter全部在image里面的时候，进行卷积运算**
- same padding：**当filter的中心(K)与image的边角重合时，开始做卷积运算；卷积之后输出的feature map尺寸保持不变**

# 中级

Q9：****Pooling有哪些不同类型？说明他们的特点。****

Q12：**解释flatten层在CNN中的角色和作用**

Q13：****列出池化层的超参数****

Q14：****解释CNN中“参数共享”和“稀疏连接”的意义****

Q15：**可以使用CNN执行降维操作吗？如果可以，CNN中哪个相关子层执行了降维操作？**
