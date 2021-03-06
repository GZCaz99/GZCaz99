# Intro
Resamplinng methods. 包括了从训练集中重复采样再重新拟合模型并从此获得更多信息的过程。2种最常见的重复采样方法分别是 ***Cross validation*** 以及 ***Bootstrapping*** :
- ***Cross validation*** 包含了以下两种主要应用：
  - Model assessment: 对于一个给定的统计学习方法来估算他的错误率， 从而了解/评估它的表现
  - Model selection : 选择一个拥有合适自由度的模型
- ***Bootstrapping*** : 用以测量对应参数/统计学习方法的准确率

在现实工作中， 计算test error rate 需要一个与训练数据集非常相似的测试数据集， 但一般我们都没有。 这时我们采用一种数据留用的方法来测试我们的模型， e.g 假设训练集中有1000个输入数据， 我们取其中20%
作为测试数据留用， 将剩下的80% 数据用作训练集来拟合模型，我们这时需要考虑的问题就是如何确定这需要留用的数据数量/比例。 在这个概念下延伸出3种常用的方法：
- The validation set approch:  将原训练集随机比例分为两个部分，即新训练集以及测试集， 在新训练集的数据中建立模型， 再将这个模型应用于测试集中观察模型表现。
  - 然而， 因为该方法基于将原数据集按随机比例分配，所以每个比例最后得出的错误率也不相同， 即错误率在不同比例之间的变化率较高，而且因为一部分的数据被留用做测试集，会导致我们的数据量降低。
- Leave one out cross-validation（LOOCV）:该方法原理上与上面的方法相同， 具体不同在操作上， 为了减少方法带来的不稳定性以及训练数据量的减少， 该方法采用了以下算法：
  - 1, 将长度为 N 的原数据集分为长度为 N-1 的训练集 以及 长度为 1 的测试集。
  - 2， 用训练集来拟合模型
  - 3， 将模型运用于测试集， 求出对应的错误率
  - 4， 重复上述过程 n 次
  - 5， 模型的错误率就约等于 n 次测试错误率的平均值
  - 相较于上面的方法， 该方法拥有更小的 bias, 错误率变化， 但计算强度上更高
- k-fold cross validation: 该方法具体操作如下：
   - 1， 将原数据集随机分成长度大致相等的 k 组子数据集（kth fold）
   - 2， 第一组将留用作为测试集， 剩下的其他组的数据则作为训练集来用于拟合模型。并应用于测试集中计算错误率
   - 3， 在每一组中重复上述过程，即k次，每次都有一个 kth 组被留用作为测试组。
   - 4， K-fold cross validation 错误率即是所有组别都遍历一次之后的错误率的平均数。

总的来说， LOOCV 比 k-fold 拥有更小的 bias和更大的方差(当k<n时)，经验上已经证明当 k=5/10 时， k-fold 是最好的测试方法， 它有更精确的错误率， 也能达到更好的 bias-variance 平衡.
上文所介绍的基本都是对于回归问题， 而对于分类问题，我们需要求出一个分类模型的误判率， 此时有：
>![image](https://user-images.githubusercontent.com/89850899/162237424-18b9e3ed-9857-4022-af22-1beafa034c79.png)
