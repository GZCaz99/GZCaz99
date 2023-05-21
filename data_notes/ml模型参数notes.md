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

### 梯度下降
通常我们会通过一个叫做 Grid Search 的过程来确定一组最佳的参数。其实这个过程说白了就是根据给定的参数候选对所有的组合进行暴力搜索。
>param_grid = {'n_estimators': [300, 500], 'max_features': [10, 12, 14]}

>model = grid_search.GridSearchCV(estimator=rfr, param_grid=param_grid, n_jobs=1, cv=10, verbose=20, scoring=RMSE)

>model.fit(X_train, y_train)
顺带一提，Random Forest 一般在 max_features 设为 Feature 数量的平方根附近得到最佳结果。
这里要重点讲一下 Xgboost 的调参。通常认为对它性能影响较大的参数有：
- eta：每次迭代完成后更新权重时的步长。越小训练越慢。
- num_round：总共迭代的次数。
- subsample：训练每棵树时用来训练的数据占全部的比例。用于防止 Overfitting。
- colsample_bytree：训练每棵树时用来训练的特征的比例，类似 RandomForestClassifier 的 max_features。
- max_depth：每棵树的最大深度限制。与 Random Forest 不同，Gradient Boosting 如果不对深度加以限制，最终是会 Overfit 的。
- early_stopping_rounds：用于控制在 Out Of Sample 的验证集上连续多少个迭代的分数都没有提高后就提前终止训练。用于防止 Overfitting。

一般的调参步骤是：
1. 将训练数据的一部分划出来作为验证集。
2. 先将 eta 设得比较高（比如 0.1），num_round 设为 300 ~ 500。
3. 用 Grid Search 对其他参数进行搜索
4. 逐步将 eta 降低，找到最佳值。
5. 以验证集为 watchlist，用找到的最佳参数组合重新在训练集上训练。注意观察算法的输出，看每次迭代后在验证集上分数的变化情况，从而得到最佳的 early_stopping_rounds。

最后要提一点，所有具有随机性的 Model 一般都会有一个 seed 或是 random_state 参数用于控制随机种子。得到一个好的 Model 后，在记录参数时务必也记录下这个值，从而能够在之后重现 Model。

### Cross Validation
Cross Validation 是非常重要的一个环节。它让你知道你的 Model 有没有 Overfit，是不是真的能够 Generalize 到测试集上。在很多比赛中 Public LB 都会因为这样那样的原因而不可靠。当你改进了 Feature 或是 Model 得到了一个更高的 CV 结果，提交之后得到的 LB 结果却变差了，一般认为这时应该相信 CV 的结果。当然，最理想的情况是多种不同的 CV 方法得到的结果和 LB 同时提高，但这样的比赛并不是太多。在数据的分布比较随机均衡的情况下，5-Fold CV 一般就足够了。如果不放心，可以提到 10-Fold。但是 Fold 越多训练也就会越慢，需要根据实际情况进行取舍。



### PCA 降维
from sklearn.decomposition import PCA

### random forest/Extra Randomized Trees
### XGboost

## 以下模型往往在性能上稍逊一筹，但是很适合作为 Ensemble 的 Base Model
#### SVM
> https://tengzi-will.github.io/2019/04/25/%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0%E5%AE%9E%E6%88%98-%E6%94%AF%E6%8C%81%E5%90%91%E9%87%8F%E6%9C%BA-SVM/
#### Neural Networks
#### Logistic Regression
#### Linear Regression
