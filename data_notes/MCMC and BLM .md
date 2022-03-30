# MCMC
### 后验分布回顾
贝叶斯推断围绕着后验分布P（theta｜x）进行。
### Monte carlo Markov chain 
Gibbds smapling 是其中一种在MCMC中常用的后验取算法， 它的大致流程如下：
>![image](https://user-images.githubusercontent.com/89850899/160603813-370f4149-6108-43c1-b5de-41da47287f45.png)

要注意的是， 该算法中应用了 Full conditional distrbution 来取样， 可以理解为，例如一个正态分布， 有两个参数 theta1 = mu/theta2 = sigma^2, 对应的取样分布在Gibbs 中就是：
> Sample theta1 from P(t1|t2,x) ；theta2 from P(t2|t1,x), 即所有参数都是 conditional on the other.

### Convergence Diagnostics
在进行MCMC 取样时，特别需要注意的一点是最终样品是否Converge，即取样的分布是否均匀。 一般来说， MCMC的结果最后会趋近平均分布， 例如：
>![image](https://user-images.githubusercontent.com/89850899/160674368-5fad4da0-3011-4d7a-9301-2a0cc0fd8dcf.png)
 
随着迭代次数的增加，MCMC所取的值会越来越接近于属于同一个分布， 即越来越接近与从相同的分布里取值。 而在迭代初期的取值分布是混乱的， 所以我们需要舍去迭代初期所取的值。例如下图：
>![image](https://user-images.githubusercontent.com/89850899/160674899-e7b81bb5-abdd-47cf-9317-05b03dd39f68.png)

>我们可以看到，在粉色区域之后的值越来越稳定，这个区域称为 burn-in area， 在这个区域里的值是混乱的，也是我们需要舍弃掉的。

在MCMC中，确定这 burn-in area 的区间就是我们检查模型是否converge 的必要步骤。其中一种方法就是上图所示的， 将 value/iteration plot出来， 肉眼观察取值波动从而确定区间， 即iteration<x的值我们舍弃掉。另一种更加常用也精准的方式就是使用 Gelman-Rubin Diagonstics, 它本质上是对同一个chain应用不同的initial value, 生成不同的后验sample， 在来比较这些value/iteration plot 的去掉burn-in的结果， e.g:
>![image](https://user-images.githubusercontent.com/89850899/160688174-a345e02b-2401-48c6-9980-05fd578f8bc0.png)

图中展示了是三个不同的initail value 生成的chain， 可以看到在一定次数的迭代后， 他们的取值都越来越稳定/趋近于同一个分布。 是否converge在GRD中由比较取值的Inter-chain以及Within-chain variability 决定。 Inter-Chain 指计算一个迭代区间（e.g 100次到200次）内，应用了不同的initial value生成的值的波动， 而Within-chain 指的是不同initial value生成的chain的取值分布/波动（e.g 上图中红线/蓝线在burn-in之后的取值差别）。GRD 会生成一个 Scale reduction factor, 当该参数等于 1 时， 说明之前的两个variability相等，而该值较大时则代表chain 之间有值得注意的差别。一般来说， 当这个值大于 1，1 时，说明chain 没有convergence.在R中， GRD 可以通过 coda 包中的gelman.diag() 来调用， 中间带入建好的jags模型就行， 在结果中， upper C.I 接近于1 说明chain is converged, 或者至少不大于 1.1（或者1.05）。 之后我们可以visualise 检测结果， 通过指令gelman.diag(), 它能够帮助我们更好的选择需要舍弃的迭代次数以及对应的取样。还有一种converge可视化是通过traceplot（）,它会生成jags中储存参数的Trace/iteration 和 Density/estimate 这两种图，通过观察第一种图中图形是否均匀分布，第二种 density图则能更加直观的告诉我们 chain 是否属于同一分布。 Rhat 就是缩减系数。

当chain并不converge时， 我们需要检查JAG model 是否正确建立，如果JAG建模没有问题却仍然无法converge，我们则需要检查以下：
- 增加迭代次数
- 选择更好的initial values
- 改变variables, 例如将covariate xi 转换成 （xi - mu），这一步称为 Centring. 或者 Standardizing, 即（xi - mu）/sigma。 这两种方式都可以有效帮助converge

在

