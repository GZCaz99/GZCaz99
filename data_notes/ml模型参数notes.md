## 模型具体调用方法/参数的笔记 ##
机器学习问题，大致包含这是哪个方面：
  - 模型：建立什么样的模型
  - 目标：怎么定义最大化或最小化的目标函数
  - 算法：怎么求解最大或最小化目标函数的优化问题
也可以说,模型训练的本质,就是通过训练找到一系列模型参数 $\beta^*$ , 使得损失函数值最小化.

### 损失函数 ###
损失函数（loss function）是用来估量模型的预测值f(x)与真实值Y的不一致程度，它是一个非负实值函数,通常使用L(Y, f(x))来表示，损失函数越小，模型的鲁棒性就越好。损失函数旨在表示出logit和label的差异程度，不同的损失函数有不同的表示意义，也就是在最小化损失函数过程中，logit逼近label的方式不同，得到的结果可能也不同。
一般情况下，softmax和sigmoid使用交叉熵损失（logloss），hingeloss是SVM推导出的，hingeloss的输入使用原始logit即可。机器学习的目的，就是在确定好模型（假设集）的前提下，构建目标函数构建优化问题，然后通过优化算法求解模型的最优参数
> https://cloud.tencent.com/developer/article/1165263
> https://blog.csdn.net/heyongluoyao8/article/details/52462400
> 线性回归与损失函数例子 https://blog.csdn.net/xiazdong/article/details/7950084


### PCA 降维
from sklearn.decomposition import PCA
