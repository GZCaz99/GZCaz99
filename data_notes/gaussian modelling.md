# Gaussian process/ modelling
#### 这里主要记录高斯建模/时空间建模的笔记

## Week 2
多维高斯：Y(x)~GP(mu(x),C(x1,x2,...))，  Mu(x) = a+bx+cx^2,现在是： Mu(x1，x2,...) = a+b1x1+b2x2+c1x1^2.... 增加了稀疏的维度， 由1d(一个点)到2d（一个向量）
kriging:一个模型的子集， NO distribution/assumptions, variagram, Best linear un-bias predictors, parameter space(mu,sigma,length_index), using method of moments
- Variagram:

     2gamma(h) = E[(y(xi+h)-Y(x))^2] = Var[Y(xi+h) - Y(x)]
     with Var[x] = E[x^2] - E[x]^2
     thus 2gamma(h) = Var[Y(x+h)] + Var[Y(x)] - 2Cov[Y(x+h),Y(x)]
                    = sigma^2 + sigma^2 - 2C(h), C(h) = distance function 
                thus, gamma(h) = sigma^2 - C(h), fitting the curve by weitgted leaste square: 
                min(model para:sigma theta residual) sum(wi*gmamma(hi)[sample var] - gamma(theta)[median]]^2
                将数据划分为一个个小区间（x1,x2）对这个区间里的数据求平均值，这样这个区间里就只剩一个平均值的点，重复这个步骤至所有区间，最后将所有平均点练起来，这条线就是fitted line
 今天讲了一点krigin， 回家再看lecture
 
GP:assume all is nomally distributed, covariance fun., MVN for interpolation , parameter space(mu,sigma,length_index), using MLE as there's distribution/Bayesian 

有一个输入空间
