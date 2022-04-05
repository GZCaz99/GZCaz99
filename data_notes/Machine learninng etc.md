# Machine learning Intro
假设我们有一些观测到的 Yi 和 Xi, 它们的关系可以用下式子描述：
> ![image](https://user-images.githubusercontent.com/89850899/161816161-e993d4ab-1803-4821-8987-3763ff9191fb.png)
绝大部份的机器学习问题可以被分为两种：
- Supervised learning : both the predictor Xi and the response Yi are observed 
- Unsupervised learning : Xi is observed while Yi is nnot, we need a model to predict Y

### Supervised learning algorithims 
监督学习算法使用labelled examples， 即输入和需要的输出是已知的（being labelled）.它用于学习patterns, 再将其应用于新的， unlablled data. 监督学习算法可以被分为两大类：
- 回归算法
  - 适用于当response Y 是连续的数值时. e.g 某件物品的未来价格..
- 分类算法 Classification
  - 用于当Y 是分类的/离散的. e.g 某件物品未来是涨价/降价
 
## 回归模型拟合度
回归算法常用的拟合度指数可以通过MSE计算出来， 即：
>![image](https://user-images.githubusercontent.com/89850899/161818096-99cdfde1-ccc4-453e-a606-cfe18b4ff1d5.png)

大致上我们倾向于模型拥有最小的MSE， 但我们更看重模型在应用在新数据的表现。相似的， 对于新数据，自然也有一个MSE值 test MSE，通过比较不同的MSE值可以了解模型的表现。 但当我们没有额外的测试数据时
就需要引进 Model flexibility 的概念， 它指一个模型的自由程度。在广义线性模型的学习中，一个模型的自由度越高， 对于数据变化的表现就越好， 对应的MSE就越低。 但是过高的自由度对于对应的数据集可能表现良好， 但当作用在其他数据集时可能表现糟糕，现实中，随着模型的自由度增加， training MSE 会越来越低，但随着之后应用于不同测试数据集的次数增加， test MSE 则会越来越高：
> ![image](https://user-images.githubusercontent.com/89850899/161820570-51545bd3-8466-4fcb-bc78-a70414f5b6cb.png)

总的来说， 过高的模型自由度会引起过拟合的发生， 即模型在描述变量的关系之外也包括了随机因素（noise）。当我们的出发点是模型推断时， 更应看重模型对数据/变量的解释程度， 而模型的自由度越高， 对真实数据的解释程度就越低， 如何平衡这两点是我们需要考虑的

## Bias and variance trade-off
- bias ： 一种由数据/样本整体偏差产生的error， 模型的自由度越高 bias 越低
- Variance： 模型运用于不同样本间产生的预测结果的差异。 
总的来说， 模型的自由度越高，bias 越低， variance 越高

## Expected test MSE
>![image](https://user-images.githubusercontent.com/89850899/161850367-9f9852a0-c205-42cc-a950-ec1d2522809b.png)

我们面对的挑战就是建立一个同时具有 low variance/low bias 的模型


## Classification
对于线性回归的模型拟合度， 我们可以使用MSE来判断， 而对于分类模型， 我们应用 error rate:
>![image](https://user-images.githubusercontent.com/89850899/161851369-cc3da9bd-7109-4e3b-8aad-a2ca5078fa2e.png)

Error rate 表示了模型结果中误判的部分， 上式为train error rate,  相似的， 在判断分类模型的优劣时我们也需要同时观察它的test error rate。理想情况下， 错误率越小越好。

## Bayes classifier
对于一个数据集， 贝叶斯分类计算：
>![image](https://user-images.githubusercontent.com/89850899/161852875-6c601302-1b5d-4272-8461-9f60a094c356.png)

贝叶斯分类具有最小的 test error rate, 即 bayes error rate:
>![image](https://user-images.githubusercontent.com/89850899/161853458-6af94f2c-4ff0-4afe-b258-b60d481a9d9a.png)

## K-Nearest neighbour



