# General Additive Models (GAM)
## Intro of Non-parametric model
在上一章节中的 GLM 中， 我们学习了 GLM 的结构和特点。 相较于GLM， GAM中将 *Linear predictor* 这一项 替换成了一个集合了一系列未知参数的函数：
> <img width="344" alt="WeChat8137ecc147d890b546a32cc63e5bb010" src="https://user-images.githubusercontent.com/89850899/158422113-14e33e72-ae58-4111-b1ad-b7de41c9bc93.png">
其中 *F()* 是 *smooth function*，它是一个*Non- parametric function*， 即不对模型做出任何基于分布/数据趋势的假设。相对于之前的参数化模型，即假设一个模型为：
> ***y = b + b1X1+...*** 这种基本线性模型， 或者是 ***mu =eta= b + b1X1+...*** 这种GLM中的针对指数分布的数据的模型。

以上模型均假设了一种或者多种线性/非线性关系。相较于它们，非参数模型拥有更高的自由度，对数据也更加贴合， 然而其过高的自由度会带来过拟合的问题，在进行回归建模时需要的数据量更多，在进行预测数据集之外的值时表现也欠佳（e.g 饱和模型就是一种最终极的非参数模型）。最后，还有一种***semi-parametriparametric model***.它指的是一种不提前对***µ(xi)*** 的函数进行任何假设的模型， 即我们在不估计模型参数值，直接对***µ(xi)*** 进行估计。这是一个相对复杂的过程，我们一般始于假设***µ(xi)*** 为一个smooth function，即一个continuous and has continuous derivatives up to a certain order (it is differentiable and its derivative is a continuous function)，一个最直观的例子是：
> ***aX<sub>1</sub> + bx<sup>2</sup><sub>2</sub> +cx<sup>3</sup><sub>3</sub>+.....***

## 1 General Additional Model(GAM)
### 1.1, Intro
由GLM扩展而来， 结合上述的定义， 一个加性模型的通常形式为：
>![image](https://user-images.githubusercontent.com/89850899/159052904-9d0cbac0-830e-4282-8efb-8e77deaf9f68.png)
其中 x = (z, x1, . . . , xp), z,是linear predictor, fj(·)是smooth function

一个简单的例子：假如我们想要调查某个connty在温度低于5度时的平均用水需求，在掌握了相关的数据后， 一个简易Additional模型可为；
>![image](https://user-images.githubusercontent.com/89850899/159053991-3e963a19-6061-4bf5-83a9-3b0bf593bbc7.png)

>其中，当温度高于/低于 5度时， 对应的 z = 0/1, f(x) 为smooth functiofunction，它允许了在除了已经应用covariate之外的response factor的波动， 从而能够给出我们一些潜在的取样建议。

在加性模型中，我们需要特别关注对应smooth function的应用， 以及它的smooth程度。在R中通过应用**penalized regression splines** 来表示smooth function， 从而对基于数据进行**cross validation** 来得出合适的smooth程度。这方法的前提是选定一个合适的 ***basis function***：
>![image](https://user-images.githubusercontent.com/89850899/159059978-3a55acd8-80f0-420e-91d8-9d545f179ad5.png)

简易的例子是：
>![image](https://user-images.githubusercontent.com/89850899/159060315-1f44dc5f-3c21-48d2-b8c1-c9acb815ccea.png)

>其中are b1(x) = 1, b2(x) = x, b3(x) = x2...
在 bs 中还有两个特别重要的参数， *K（knot）* 以及 *q（rank）* 。 K值可以理解为由smooth function画出来的线的peak的点的数量，也是function中参数的数量，而q就是k-1.

#### **penalized regression splines**
为了防止过拟合，GAM在最小二乘的方式上额外添加了一个‘wiggle coeffition’：
> ![image](https://user-images.githubusercontent.com/89850899/159153702-8f0c9ca9-7e2b-4a2f-9cd4-c7607b8bfb01.png)

>可以理解为最小二乘的值额外加上了一部分‘负担’，从而避免过拟合。 其中lamda就是smooth parameter,可以看到lamda越大，最后画出来的线就越接近一条直线，lamda越接近0，结果就越无限贴近元数据，即接近无意义的饱和模型的结果。

前文还提到了通过*cross validation*来选出一个合适的lamda，而交叉验证本质上是一个数据子集（e.g 预测值）与原母数据集的偏离程度，为此我们需要估计一个理想的lamda值来最小化这个偏离程度。


### 1.2 GAM in R
GAM 在R中的应用基本上与GLM一致，一开始的模型参数指定：
>![image](https://user-images.githubusercontent.com/89850899/159066383-e183a3d7-e598-4dc9-b801-9b871af9e31e.png)

>其中K值/bs/familiy 的应用选择上可以根据情况改变。bs一般选择的是cubic spline，指令为**cs**。
>![image](https://user-images.githubusercontent.com/89850899/159152808-d9d2d936-23a6-444d-8304-d27109d32a99.png)

>相较于GLM模型的结果，GAM的结果包含两个部分，第一个部分是***Parametric coefficient***，即对模型中intercept参数的总结，第二个则是***Significance of smoothe terms***,展示了smooth function的结果。

在之后的模型参数推断中， 根据上面得到的模型结果，可以分别得出估计的模型的方差，rank,smooth function 中的参数，lamda，具体操作可以参考如下：
> ![image](https://user-images.githubusercontent.com/89850899/159154472-4881f84e-6486-47c8-b71c-809d42382236.png)

模型预测的方法与GLM基本一致，之后我们可以进行模型检测：
>![image](https://user-images.githubusercontent.com/89850899/159154571-6c5a1f18-e35f-4d3f-bc43-a60288643abc.png)

检测的结果有两部分组成，第一部分为residual plot，其中一共有4张图，需要注意的是：
- 左上角的 Q-Q plot， 如果模型表现良好的话，所有的残差点应该都沿着斜线分布
- 右上角的 residuals vs the fitted values，对于一个优秀的模型，我们应该看到图中残差值均匀分布在0两侧，而不应该有其他任何趋势。
- 左下角的 histogram of the residuals，它用来表示残差值是否服从正态分布。
- 右下角的 response (Yi) versus the fitted/predicted values (Yˆi)，它与第一张图基本一致，对于一个合适的模型，残差点应沿斜线分布。


在残差图之外，我们还有一个对于模型中所应用的smooth function 的结果总结：
- k', 即k-1
- edf,它的值表示了在设定的参数中真正被应用于smmothing的参数数量，即最终被用来确定数据关系/贴合模型需要的参数数量。一个常用的点是，当k‘与edf的值相差小于1时，说明我们需要增加k值（模型自由度）
- k-index/p-value, 这两个数值不是正式test，但仍给了我们对应的建议。当k-index/p-value 分别 小于1/数值很小 时，我们可能需要考虑增加k的数量。 它们不属于正式的检测，所以即使他们的数值建议我们增加k，我们也可根据前面的其他检测结果来证明模型的合理性。

在确定了k和其他一些设定后，我们可以进行LRT，通过与饱和模型对比来检测我们模型的最终效果，大致理论与方法在上一章GLM中已经介绍，具体差异如下：
> ![image](https://user-images.githubusercontent.com/89850899/159159543-cdcfd124-2867-4b5b-9a67-40151ba41d69.png)

其中，residual degrees of freedom (n − EDF) 代替了之前GLM中的模型自由度。 它需要从模型中提取，指令为 model$df.residual. 最后我们来进行LRT:
> ![image](https://user-images.githubusercontent.com/89850899/159159649-fffcb274-77c9-4870-b40b-b9aa539f10f5.png)
如果 P-value 大于 0.05，说明基于对应的lamda，我们的模型表现良好。

最后，不同的GAM模型之间效果的比较主要通过一下三步来检测：
- plot（）,这个指令在GAM中会画出smooth function 的结果， 可以通过它与原数据的图比较，直观的得出所应用的smooth function 的显著性
- summary（）, 通过它得到模型中每个smooth function 的总结，以及相关参数的显著性
- AIC()，通过它来最直接的对不同模型进行比较， AIC更小的模型表现更好。











 
