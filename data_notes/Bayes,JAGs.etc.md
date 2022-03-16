# 贝叶斯， JAGs和一些其他统计杂学

## 1, Bayes theorem 
传统统计中， 将未知的模型参数看作是一个固定的常数，而数据则是随机变量，使用MLE来估计最可能的模型参数。而贝叶斯派中，则完全相反，将数据看为是固定的常数，而模型参数则为一个随机变量，进而研究改模型参数的分布情况。贝叶斯统计中包含了***Prior***， ***Likelihood***， ***Post-Prior*** 这三种关键变量， 一个贝叶斯统计的过程包括了基于提出的***Prior*** 以及通过数据求出***Likelihood***， 再结合两者求出***Post-Prior***的过程， 随着这个步骤的不断重复， 得到的***Post-Prior***也会越来越准确。
## x, JAG 在 R 中的运用
Monte Carlo 在R中的实现主要通过 JAGs（Just another Gibbs sampler） 实现, 为此我们首先需要安装一些相关package：
> ![image](https://user-images.githubusercontent.com/89850899/158208344-e1e653d5-48f0-466a-9000-fcafa3553139.png)
接下来， 通过这些package 来建立 Bayes model的流程如下：
- 1，定义 ***JAG*** 模型，即建立它的 function
- 2，准备/整理数据
- 3，定义我们需要的 posterior-distribution 参数
- 4, 定义JAG function 的初始值， initial values needs to be passed as a list
- 5, Fit the model in JAGS. The most important arguments of the jags function includes: data (data
list), inits (list of initial values), parameters.to.save (parameters of interest), n.chains (number of
MC chains - each gives a sequence of simulated values), n.iter (number of iterations in the sampling
process), n.burnin (number of initial samples to discard), model.file (the JAGS model definition).
- 6，Convergence diagnostics
- 7.Once we are satisfied that the chains have converged, we can start the statistical inference. 

