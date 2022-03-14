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

#### 1.2 Normal GLM
如上文所所示， Normal distribution 属于 Exponential Family， 而他的 mean 与 covariate 也是linear关系，所以自然也可以直接运用GLM函数，具体操作如下：
><img width="848" alt="WeChatc8a843ee7e1b254f27e299eb8cfff84a" src="https://user-images.githubusercontent.com/89850899/157471185-67218bc1-743e-4d39-9edc-054655d57509.png">

需要注意的是其中：*family* 一项为 *gaussian*， 因为正态分布本质上就是高斯分布的简化， 另外后面的 *link = idendity* 是因为对于正态分布， 它的*linear predictor η<sub>i</sub>*
就等于*link function g()*. 下一个需要注意的是 Dispersion 参数 *phi*，在GLM中它的值是通过 ***deviance/(n-p-1)*** 得出的， 而在这个正态分布的例子里， 它就等于*Var*， 所以它也应该和*residual standard error* 相等。

#### 1.3 Parameter inference
在上一章中，我们使用*Z-test* 和它的结果来进行*Hypothesis test* 并求出 *C.I*, 这是基于我们已知*φ*的分布的前提下求出的，而在*φ*的分布未知的情况下，我们则需要应用*T-test*来进行*Hypothesis test* 和求出*C.I*. 在R中的指令为：
>![image](https://user-images.githubusercontent.com/89850899/157667906-4ed01892-4fbd-4851-9eb9-d088353b8448.png)

而同样的，如果求出的*P-value* > 0.05, 那门我们就在 95% 这个level上***Reject*** the null hypothesis. R 也会自动选择要应用的 test 类型。

#### 1.4 Model checking
GLM的模型fitness检验大致与上一章内容相符，稍微不同的点在于：
> ![image](https://user-images.githubusercontent.com/89850899/157685155-d68d8880-53fd-4ce8-8d0d-3d6346900001.png)
>![image](https://user-images.githubusercontent.com/89850899/157685239-d3fe3306-c3bd-45b1-9cae-ac789894ff76.png)

而需要特别注意的是，对于未知*φ*的分布（Normal，Gamma），进行fitness检验的意义不大，因为算法会自动选择一个合适的估计值*φ-hat*，使得检测值最贴近饱和模型的值，所以对与上述分布来说我们需要额外观察它的***Residual***分布情况。对于其他*φ* 已知的分布（Binomial, Poisson, Exponential），该检验则有效。

#### 1.5 Model Comparison
大致上的模型对比过程也与上一章相同， 需要注意的是：
>![image](https://user-images.githubusercontent.com/89850899/157687739-8a88ba37-922c-47dd-97ad-ee5d6fddf202.png)
>![image](https://user-images.githubusercontent.com/89850899/157687847-6e3e6ed8-f67c-4082-9cc8-aeb8f4b49a06.png)

正如前文所提，上述分布对应的是*φ* 已知的分布（Binomial, Poisson, Exponential），而对于未知*φ*的分布（Normal，Gamma），则需要一个合适的估计值*φ-hat*：
>![image](https://user-images.githubusercontent.com/89850899/157688309-163d0c3c-1d68-40de-a5ce-814a1a7ae26c.png)

因为一个估计参数的加入，我们需要使用***F-test***：
>![image](https://user-images.githubusercontent.com/89850899/157688663-2e7e4f42-8d75-40f9-be54-71944060b1b6.png)

其中 *p2 − p1* 是*first degree of freedom* 而 *n-p2-1* 是 *second degree of freedom*. 在R中操作可以参考样例：
>![image](https://user-images.githubusercontent.com/89850899/157689226-182fe091-bdf1-49c8-ba6d-6003adb59a03.png)

或者，也可以使用anova：
>![image](https://user-images.githubusercontent.com/89850899/157689734-a3a66410-8c42-4929-bf62-8418d8a98f93.png)

同样的，如果求出的 *P-value* < 0.05, 则***Reject*** the null hypothesis.

## 2, Binomial GLM
对于 Binomial 分布的数据， 大致的建模思想与上一章相同， 即对成功的次数进行建模，为此需要应用 *Logit* 函数将 mu 固定在 0～1 的区间内， R中的操作如下：
> ![image](https://user-images.githubusercontent.com/89850899/157694682-a88629d7-5f58-4f19-99c4-9bb3daf2f59f.png)
>![image](https://user-images.githubusercontent.com/89850899/157694773-7d9f841e-bc3b-4bc9-8e6e-5c42e17dd6ae.png)

需要注意的是 Binomial 对应的 link function 是 logit。

#### 2.1 Parameter inference
因为 Binomial 中的*φ* = 1， 所以只需要使用 Z-test 即可，之后再在基础之上求出对应的 C.I

#### 2.2 Model Checking
这部分也比较简单， 因为*φ* 已知所以不需要估计，案例操作如下：
>![image](https://user-images.githubusercontent.com/89850899/157696318-85d119d8-52ce-4a3a-b12d-e4abc91890cb.png)

同样的，*P-value* < 0.05, 则***Reject*** the null hypothesis. 另外，当数据总数较小时，我们需要应用 ***Pearson residuals*** 来代替原来的 ***deviance residuals***， 具体操作参考下图：
>![image](https://user-images.githubusercontent.com/89850899/157698260-3b559d0f-6350-47df-9fae-e1f7f74656a7.png)

#### 2.3 Prediction
使用模型预测的理论在上一章中已有介绍，一般来说步骤可以分为：

- 1，Plot ***模型对应的*** Response variable 和 Covariate（plot1）
- 2，建立一个用于预测的 ***Covariate*** 向量/区间
- 3，应用R中的 *predict* 生成对于 ***Response variable*** 的预测值(type = response)
- 4，将2，3中建立/预测到的 variable值 plot 出并插入 1. 的plot 中， 可查看模型贴合程度
- 5，再次应用R中的 *predict* ， 但这次生成对于 ***linear predictor*** 的预测值(type = link)
- 6，对于5. 中得到的预测值建立对应的 C.I, 并将 C.I 代回 invert logit function 得出最后的 Upper/Lower limit
- 7，将6. 中得到的limit 和 3,中使用的值分别plot出预测的 Upper/Lower limit 并插入 plot 1。 这样，我们最终得到了预测出的*E(x)*的平均值以及它的C.I
- 8, 现在我们可以利用3，中得到的值来进行 P.I 及其Upper/Lower limit的建立。在这里首先我们 Plot ***数据*** 的Response variable 和 Covariate（plot 8）
- 9，有了3，中的预测值，它现在就是我们数据的***Predict distribution***，根据数据分布类型的不同，它可以是***Respons Variable***的 平均值 或是 某些数据中代表的***事件发生的概率***，这取决于数据的分布类型，不同类型分布有不同的 E（x） function. 在本案例中， binomial distribution 有 **E[x] = np**,所以这里的预测值为 *p*. 我们这里将E[x]plot出并插入plot 8 中， 这里使用的 x input仍是 3,
-10， 这次，对于***Predict distribution*** 的对应的 ***P.I*** 建立，我们需要考虑到原数据的分布类型，对与本次的BInomial 分布数据，我们使用：![image](https://user-images.githubusercontent.com/89850899/158026091-790175c5-9869-4365-ab98-ff51713a834e.png) 

来模拟数据分布情况，以及求出 P.I 的区间， 最后将这几条线plot在 8，的图中，就可以得到最终的预测结果。
#### 2.4 Residual Checking
除了之前提到的几个模型检查的理论之外， 模型表现也可以通过检查对应的 Residual 分布来评判。 一般来说， 任意模型的 Residual plot 有以下几张图：
> ![image](https://user-images.githubusercontent.com/89850899/158196154-3f3906cc-2616-437b-a542-760ca1cb5aa2.png)

其中， 左上角为 ***Deviance Residual vs Fitted***， 如果一个模型的表现良好，图中的点应随机，均匀分布在 0 周围。而如果点呈 *漏斗状*分布， 则表明数据的方差大于模型包括的， 如果还有其他的明显的分布趋势， 我们则需要考虑调整模型中的 *covariate* 或者 其他高阶模型（当数据是Binary分布时则不需要过多关注）。 接下来是右上角的 ***Q-Q*** plot, 它可以用来判定模型的 Residual 是否属于正态分布，如果是，则图中点会沿图中虚线分布， 如果有其他的系统性分布，则说明我们的模型有问题。左下角的图本质上与左上角的没有区别，我们这里跳过。最后一张是***Residual vs Leverage***，这张图展现了数据中的***极值***， 它为我们移除一些数据集中不合适的数据提供了帮助， 但并不应该只基于这张图来剔除数据。




 





