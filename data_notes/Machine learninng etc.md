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
就需要引进 Model flexibility 的概念， 它指一个模型的自由程度。在广义线性模型的学习中，一个
