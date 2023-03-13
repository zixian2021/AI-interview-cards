# PCA

Q1：***什么是PCA***？

- ***PCA***通常用于*降维*，它对高维度数据集合寻找尽可能少的正交矢量（主成分）表征数据信息特征。
- 主成分是一系列单位向量，主成分的方向是使投影数据的方差最大化（代表最大信息量）的方向。

Q2：****可以使用*PCA*进行特征选择吗？**  

- 特征选择是指从完整的特征集中选择特征的子集；而PCA通过定义主成分，定义了一组新的特征来反映数据集中的大部分信息，新特征不等同于原始特征。因此PCA不是一种特征选择方法。

Q3：*****PCA*中的第一、第二个主成分轴是如何选择的？**  

- 最简单的方法是找到使方差最大化的投影。第一主成分是**空间中投影具有最大方差的方向**。第二个主成分是在与第一个正交的所有方向中最大化方差的方向。

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

Q4：***为什么在执行PCA之前标准化数据很重要？***  

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

- 标准化数据使得特征处于同一数量级，具有不同数量级值的特征会影响 PCA 计算最佳主成分，因为PCA对变量的方差非常敏感

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

Q5：***PCA和随机投影（Random Projection）方法有什么区别？***  

- 两者都是降维操作，将数据空间从高维空间到低维空间映射，即在高维空间中选取一小组基向量，低维数据由数据在基向量上投影得到。主要区别在于 PCA 会通过寻找原始数据方差最大的方向来选择最佳基向量，而随机投影就是随机选择方向。
- **Random Projection方法在高维空间数据中计算效率较高**

引用：[https://www.quora.com/Is-there-any-difference-between-PCA-Principal-component-analysis-and-random-projection-when-preprocessing-data](https://www.quora.com/Is-there-any-difference-between-PCA-Principal-component-analysis-and-random-projection-when-preprocessing-data)

Q6： *****PCA和LDA方法有什么区别？*****

- LDA是有监督的降维方法，而PCA是无监督的降维方法；LDA降维最多降到类别数k-1的维数，而PCA没有这个限制；LDA选择分类性能最好的投影方向，而PCA选择样本点投影具有最大方差的方向。

Q7： ****如何执行*主成分分析 (PCA)*？**  

- 1.**特征标准化**。我们将每个特征标准化，使其均值为 0，方差为 1；具有不同数量级值的特征会阻止 PCA 计算最佳主成分，因为PCA对变量的方差非常敏感；
- 2.**计算协方差矩阵**；*协方差矩阵是一个$d$*维度的方阵，它显示了每个特征之间的成对特征相关性；
- 3.**计算协方差矩阵的特征分解**。我们计算协方差矩阵的特征向量（单位向量）及其相关的特征值（与特征向量相乘的标量）；
- 4.**从最高特征值到最低特征值对特征向量进行排序**。具有最高特征值的特征向量是第一主成分。更高的特征值对应于解释的更大量的共享方差；
- 5.**选择主成分的数量**。选择前 N 个特征向量（基于它们的特征值）成为 N 个主成分；
- 6.****沿主成分轴重铸数据：****使用由协方差矩阵的特征向量形成的特征向量，将数据从原始轴重新定向到由主成分表示的轴，这可以通过将原始数据集的转置乘以特征向量的转置来完成。

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题9*： ****在大型数据集上，你会选择使用PCA吗？还是有更好的选择？****  

- 当观测值和变量的数量非常大时，经典的 PCA 方法由于需要计算矩阵的奇异值分解，需要相当大的内存和巨大的计算时间
- 在大型数据集上，降维的更好选择有random projection、flash PCA等，flash PCA源自2014年论文《Fast Principal Component Analysis of Large-Scale Genome-Wide Data》，对代表大部分数据方差的较小数据子集执行主成分分析。

引用:[https://www.elucidata.io/blog/principal-component-analysis-on-big-data](https://www.elucidata.io/blog/principal-component-analysis-on-big-data)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题10*： *****PCA*和*t-SNE*有什么区别？**  

- PCA是一种线性降维方法，t-SNE（t-distributed Stochastic Neighbor Embedding）则是一种非线性降维方法
- PCA考虑数据中最大方差的方向，保留数据的全局结构；t-SNE通过考虑点之间的距离保留数据的局部集群结构
- PCA不涉及超参数，t-SNE涉及诸如困惑度、学习率和步数等超参数
- PCA受异常值影响大，t-SNE受异常值影响小
- 相比PCA，t-SNE的效果更好，是最好的降维算法之一

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

引用：[https://www.geeksforgeeks.org/difference-between-pca-vs-t-sne/](https://www.geeksforgeeks.org/difference-between-pca-vs-t-sne/)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题11*： ****PCA 是否会检查哪些特征是多余的并丢弃它们？****  

- PCA 不会选择某些特征并丢弃其他特征。相反，它构建了一些新特征（主成分），这些特征很好地总结了我们的一些数据点列表。当然，这些新特征是使用旧特征构建的；

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题12*： ****什么是*稀疏 PCA*？**  

- 稀疏PCA是一种专门用于统计分析和多变量数据集分析的技术。它通过向输入变量引入稀疏结构来降低数据的维度。
- 经典PCA和稀疏 PCA之间的区别在于，经典 PCA通常是所有输入变量的线性组合，而稀疏 PCA发现仅包含几个变量的线性组合。
- 因为稀疏 PCA 找到仅包含少量输入变量的线性组合，所以它在一定程度上减少了原始特征空间，但不像普通 PCA 那样紧凑（换句话说，它创建了一个稀疏特征向量）。

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题13*： *****PCA*如何用于*异常检测*？**  

- PCA将原始数据映射到低维空间之后，也可以根据数据在低维空间里的坐标来重构原始数据；假设数据样本$x_{i}$映射到$k$维空间的坐标为${y_{1},y_{2},...,y_{k}}$，基于该$k$维坐标重构的数据为$x_{ik}^{'}=\sum_{i=1}^{k}y_{i}e_{i}$，$e_{i}$为对应方向上的单位向量
- 基于异常检测的PCA依赖于重构误差。直观上理解，PCA提取了数据的主要特征，如果一个数据样本不容易被重构出来，表示这个数据样本的特征跟整体数据样本的特征不一致，那么它显然就是一个异常的样本。

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题14*： *****主成分分析*和*独立成分分析*有什么区别？**  

- 主成分分析（PCA）通常用于压缩信息，即降维。它在数学上等同于对原始变量矩阵的协方差矩阵执行特征向量分解，选取特征值最大（代表含有信息量最大）的几个维度构成主成分空间，将原始数据向主成分空间投影*。*
- 独立分量分析 (ICA)旨在通过将输入空间转换为最大独立基来分离信息。为此，ICA假设独立基之间必须是
    - 统计独立的，独立基之间互相不相关
    - Non-Gaussian，即独立分量具有非高斯分布

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)

[data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E](data:image/svg+xml,%3C%3Fxml version='1.0'%3F%3E%3Csvg fill='%23D3D3D3' xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' width='24px' height='24px'%3E%3Cpath d='M11,16.4l-4.7-4.7l1.4-1.4l3.3,3.3l8.4-8.4C17.5,3.3,14.9,2,12,2C6.5,2,2,6.5,2,12s4.5,10,10,10s10-4.5,10-10 c0-1.9-0.5-3.6-1.4-5.1L11,16.4z'/%3E%3C/svg%3E)

*问题15*： *****k-Means算法*和*PCA*之间有什么关系？** 

- 直觉是 PCA 试图将所有数据向量表示为少量特征向量的线性组合，并且这样做是为了最小化均方重建误差。而K-means 试图用少量质心向量的线性组合代表原始数据向量，其中线性组合权重必须全为零， 这样做也是为了最小化均方重建误差。因此，K-means算法可以看作是一个超稀疏的PCA。

引用：[https://stats.stackexchange.com/questions/183236/what-is-the-relation-between-k-means-clustering-and-pca](https://stats.stackexchange.com/questions/183236/what-is-the-relation-between-k-means-clustering-and-pca)

[data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E](data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 24 24' fill='black' width='18px' height='18px'%3E%3Cpath d='M0 0h24v24H0z' fill='none'/%3E%3Cpath d='M18 8h-1V6c0-2.76-2.24-5-5-5S7 3.24 7 6v2H6c-1.1 0-2 .9-2 2v10c0 1.1.9 2 2 2h12c1.1 0 2-.9 2-2V10c0-1.1-.9-2-2-2zm-6 9c-1.1 0-2-.9-2-2s.9-2 2-2 2 .9 2 2-.9 2-2 2zm3.1-9H8.9V6c0-1.71 1.39-3.1 3.1-3.1 1.71 0 3.1 1.39 3.1 3.1v2z'/%3E%3C/svg%3E)