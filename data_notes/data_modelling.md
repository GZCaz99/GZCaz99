# 数据建模笔记
##### lo k aprendio en exeter(mas k nada 👎 jjj)


### 1. Beyond linear model（logit(z)）
#### 1.1 modelling and MLE setting
 在这一章中，非线性模型的概念被引入了. 样例dataset记录了捕捉到的鱼的**长度（x）** ，**捉到的数量(N)**， **逃脱的数量(y)**， 直觉上我们会认为越大的鱼会越难以逃脱，然而数据集中有长度不同的鱼而逃脱数量相等，
 或是某些较小长度的鱼逃脱的数量反而比较大的鱼逃脱的数量还要更多地情况.为了更好的探索鱼的大小和逃脱数量的关系，我们引用**逃脱的鱼的概率（pi）= y/N**来更直观的了解具体的分布情况。 由此，因为鱼之有
逃走/没有逃脱这两种可能的event，所以该数据集可以认为服从binomial distribution，即***Yi~Bin(Ni,Pi)***. 现在，有了合适的数据分布，我们可以开始进行建模了，首先考虑一个简单的初始模型:

  >***Yi~Bin(Ni,pi).  Yi ~ 'iid', pi - [0,1]***
  
  >***logit(pi) = beta[0] + beta[1] xi*** , *logit(pi)= pi/(1-pi)*
  
其中， logit 函数是一个应用于binomial distribution 的分类方法， 主要用于估计某种事物发生的可能性。得到适用于该数据分布的建模方法后， 我们就可以开始下一步的参数估计。在资料中，MLE（最大似然估计）
方法被引用于估计模型参数，该方法的使用方法如下：

- 对于数据的分布种类， 取得对应种类的Probability mass/density function(PMF/PDF)
- 之后， 我们推算出对应的likelihood 和log likelihood 方程，并将他们带入一个function
- 设置需要估计的参数initial value
- 将initial value， 写好的likelihood function 带入***nlm*** function 中估计出对应的MLE
- 最后， 将估计的模型参数代入原方程， plot the fitted line， 看它与原数据的fit 状况

在R中， 需要特别注意的是likelihood 函数编写时的运算顺序以及对应项是否缺失。 在之后的initial value的求得上也要仔细考虑各种可行的方法， 错误/不合适的initial values 回引起nlm function报错。
在取得估计的模型参数*theta/beta*之后， 便可以求出这些参数对应的***C.I***：

```
OIM <- solve(MLE_result$hessian) # OIM - Observed info matrix
var <- diag(OIM) #提取参数的 variance
sd <- sqrt(var) #方差的平方就是 sigma， standard deviation
```

在求出模型参数的 s.d 之后， 我们可以通过：

```
C.I <- c(beta[i] + 1.96*sd[i],
         beta[i] - 1.96*sd[i])
```
来求出模型的参数C.I,从而进行下一个process.

### 1.2 model checking
在取得相应参数的估计后，我们可以对参数的uncertainty 进行进一步testing. 一般来说， 参数对应的*sd*越大，代表这个参数的uncertainty越高, 从而需要我们对其的有效性进行进一步检验.
Hypothesis test(假设检验)目前有几个部分组成，分别是：
- Z-test : ***Z～Normal（0，1）***，其中 *Z = (beta[i] - Np(null hypothesis)) / s.d[i]*. 因为Z follows **Standardized Normal Distribution**， 所以他的 **95%** 区间
会处于 -1.96～1.96. 所以当 Z 值大于这个区间时， 则 Z 为 **Extreme Value**， 此时我们可以 **Reject** the null hypothesis.
- P-value : 在Z-test 之上， 我们还可以应用P-value test， P-value 对应的是一个 Z 值是极值的***probability***， 在 R 中可以通过：

```
p_value <- 2*(pnorm(z_value, 0, 1))
p_value <- 2*(1 - pnorm(z_stat, 0, 1)) #当Z值为负数时用 1 - Z
```
当 P-value 小于5% 时， 我们可以***reject*** the null hypothesis.

检定完参数的uncertainty 之后， 我们可以就模型performance进行检定. 对于模型的优劣度， LRT（likelihoo ration test）会被应用于量化改程度：
    
    R = L1/L2
    
其中， R 的值决定了模型的好坏， if R > 1, 则 模型1 比 模型2 表现要好，vice versa，而 R 约等于 1 时则说明两个模型效果相似。需要注意的是，拥有更多参数的模型总是有更大的 R，所以当额外添加的参数不会太大的影响 R 值时， 这个参数的添加就没有太大的意义。 选出较好的模型后， 我们可以进行下一步的检验， 这次我们用一个 ***Satruated model(Ms)*** 来作为比较的对象。该模型只被应用于模型参数比较中， 没有其他的应用意义。***Saturated Model*** 的特征是它的预测值即等于**原值**， 而一般来说模型的预测值为**Expected value(E(p))**. 这样，我们可以得知：当比较模型与饱和模型的 likelihood 比值接近 *1* 时， 比较模型的拟合度很好。根据 likelihood 理论：

> ***-2logR ~ X<sup>2</sup> <sub>(n - p)</sub>***
其中 n = no. of data points , p = no. of parameter

>即 ： ***-2logR = 2(logLMs - logLM)***， 其中 logLM = log(likelihood of model M). (1)

基于这个理论，我们提出相对应的 **Hypothesis** :

> ***H<sub>o</sub> (null hypnosis): M1 is as good as Ms***

跟之前类似，如果得出的R 值超过了 -2logR 的 95% 区间， 则我们可以 **Reject** 对应的null hypothesis。
对于 **Nested** 模型， 我们的也可以不使用*saturated model*对比的方法,而是：
> ***-2logR ~ X<sup>2</sup> <sub>(p2 - p1)</sub>***    其中 p2/p1 = no of parameter of M1/M2

同样的， 我们有：
> ***H<sub>o</sub> (null hypnosis): M1 is as good as M2***

总结：我们需要看LRT的值是否超出 X<sup>2</sup> 95% 的区间， 如果超出的话, 则 P-value < 0.05, **thus the null is rejected**.

除了上述的方法外， 另外一个非常常用的方法是 ***AIC*** ：
>***AIC = -2log(LM) + 2p*** , 其中LM = likelihood of Model.  p = no. of unknown parameter.

AIC 的优势是更加通用， 不需要考虑模型是否nested. 通常来说，受测试模型的 AIC越小，该模型的 fitness 更高。

### 1.3 Predicting
预测是一个复杂且困难的过程， 一般来说， 我们从一个***Probability distribution***中生成预测值：
> ***Y<sub>i</sub>~p(theta<sub>i</sub>)***, 其中 Y 是一个 R.V, Theta 是模型参数的集合。

一般情况下， Y 的值都不是确定的(uncertainty)。 基于此，最好的办法就是求 mu， 因为***mu = E[Y]***, 而另 E[Y] = Y-hat, 就可得到与真实值最接近的估计值 Y-hat。在本章的案例数据集中，我们可以基于估计得到的**模型参数** ， 和一个给定的**鱼的大小（x）**，带入模型函数来：
- 估计对应的***鱼的逃脱概率（pi）***
- 进而求 **pi** 的 **Expected Value**， 在这里因为数据集是 *binomial distribution*, 所以 E[pi]=N*pi, pi = 根据模型和x得到的pi， N = 数据的数量（在这里是100条鱼）
- 最后使用**pi** 的期望值来估计对应的**逃脱的鱼的数量（Y）**

然而， 因为我们的模型参数也有相应的*uncertainty*，基于此之上估计得出的*pi* 和最后的 *Y* 自然也需要求出对应的*uncertainty*。根据前面的内容， 我们已经介绍了 *pi*的 C.I 和求出方法， 而对于我们最终需要预测的变量 *Y*， 有专门对应的所谓 ***P.I(Predict interval)***.


















