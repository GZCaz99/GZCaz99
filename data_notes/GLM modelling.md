# GLM modelling 
#### 这里作为广义线性模型（GLM）的笔记

## 1. Intro
***GLM（广义线性模型）*** ：
> ***Y<sub>i</sub>~N(theta<sub>i</sub>,phi)***

其中 ***Y<sub>i</sub>*** 是一个 *Response Variable*，**which come from a particular class of distributions
or data generating process, here we call the exponential family.** ***Theta*** 和 ***phi*** 则分别是***location parameter*** 和 ***dispersion parameter***。
前者联系着 *Mean* 而后者对应着 *Var*。通常情况下，**Var** 并不会独立于**Mean**，我们一般处理的概率分布中都有潜在的方差于平均值之间的联系， 基于此， 也可以认为方差是平均数的一个
***Scaled Function***。

***Exponential Family*** 中包含众多概率分布， 本文将着重总结 *Normal,
Binomial, Poisson, Negative Binomial, Exponential, Gamma* 这几种分布。总体上， 一旦我们决定了对应的分布来对数据建模，接下来就需要指定一个***Mean Function， F[mu]***:
> ***g(µ<sub>i</sub>) = η<sub>i</sub> = β<sub>0</sub> + β<sub>1</sub>x<sub>1,i</sub> + · · · + βpx<sub>p,i</sub>***, 这里η<sub>i</sub> 是一个***Linear Predictor***， 它联系着应变量Y和协变量X, 而它通过一个联系着数据µ的分布的函数 *g()* 互联， 该方程则被称为***Link Function***。

对于一个GLM， 它的*Likelihood Function* 可以被写成是：
> ![3371646835754_ pic](https://user-images.githubusercontent.com/89850899/157460416-addcfabc-1f50-4790-b509-473565b97bc1.jpg)

对于所有数据， 只要他的分布属于*Exponential Famiily*， 并且它的 **Covariate X** 与平均值 **µ** 具有线性关系， 那么这个数据集就可以被应用于上式来求得所需参数。

## 1.1 Normal GLM
如上文所所示， Normal distribution 属于 Exponential Family， 而他的 mean 与 covariate 也是linear关系，所以自然也可以直接运用GLM函数，具体操作如下：
><img width="848" alt="WeChatc8a843ee7e1b254f27e299eb8cfff84a" src="https://user-images.githubusercontent.com/89850899/157471185-67218bc1-743e-4d39-9edc-054655d57509.png">

需要注意的是其中：*family* 一项为 *gaussian*， 因为正态分布本质上就是高斯分布的简化， 另外后面的 *link = idendity* 是因为对于正态分布， 它的*linear predictor η<sub>i</sub>*
就等于*link function g()*
