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

#### 1.2 model checking
在取得相应参数的估计后，我们可以对参数的uncertainty 进行进一步testing. 一般来说， 参数对应的*sd*越大，代表这个参数的uncertainty越高, 从而需要我们对其的有效性进行进一步检验.
Hypothesis test（）







