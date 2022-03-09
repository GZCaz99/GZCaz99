# GLM modelling 
#### 这里作为广义线性模型（GLM）的笔记
***GLM（广义线性模型）*** ：
> ***Y<sub>i</sub>~N(theta<sub>i</sub>,phi)***

其中 ***Y<sub>i</sub>*** 是一个 *Response Variable*，**which come from a particular class of distributions
or data generating process, here we call the exponential family.** ***Theta*** 和 ***phi*** 则分别是***location parameter*** 和 ***dispersion parameter***。
前者联系着 *Mean* 而后者对应着 *Var*。通常情况下，**Var** 并不会独立于**Mean**，我们一般处理的概率分布中都有潜在的方差于平均值之间的联系， 基于此， 也可以认为方差是平均数的一个
***Scaled Function***。

***Exponential Family*** 中包含众多概率分布， 本文将着重总结 *Normal,
Binomial, Poisson, Negative Binomial, Exponential, Gamma* 这几种分布。总体上， 一旦我们决定了对应的分布来对数据建模，接下来就需要指定一个***Mean Function， F[mu]***:
> ***g(µ<sub>i</sub>) = η<sub>i</sub> = β<sub>0</sub> + β<sub>1</sub>x<sub>1,i</sub> + · · · + βpx<sub>p,i</sub>***, 这里η<sub>i</sub> 是一个***Linear Predictor***， 它联系着应变量Y和协变量X, 而它通过一个联系着数据µ的分布的函数**g()**互联，改


