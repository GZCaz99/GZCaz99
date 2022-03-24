# Gneralised Linear Mixed Modles

## Intro
### Random effects
到目前为止，我们讨论的模型参数都是一个未知的固定数值。然而我们也可以将其中的一些参数（e.g: intercept coe, 即b0）视作一个从一个 ‘*secondery distribution*' 中提取的一个随机变量。 这一‘次级分布’限制了参数的取值空间，从而进一步的
‘**Conditionally define**' 了最终的 Respoonse Variable Yi. 这种做法带来的就是***Random effect***。在数学上，对于一个response variable ***Y<sub>i</sub><sub>j</sub>*** ：
  >![image](https://user-images.githubusercontent.com/89850899/159179224-82d7aab3-bac9-4b88-90c9-b4761098dbe9.png)

>其中Y<sub>i</sub><sub>j</sub>是一系列的Response variable, 即共有j组Y，每组中有i个值。例如一个学校有j个班级，每个班级有i个学生。gamma 表示random effect

式子（1）表示***在对应的random effect*** 下，response variable Y<sub>i</sub><sub>j</sub> 服从一个平均数为 mu<sub>j</sub>, 方差为sigma<sub>y</sub><sup>2</sup>的分布(即Y的方差)。式子（2）表示 conditional mean mu<sub>j</sub> 等于 intercept加上 random effect。 式子（3）表示 random effect 服从一个平均数为0，方差为 random effect 方差的正态分布。其中有三个参数是固定的：intercept，Y的方差，random effect 的方差。
random effect的引入主要有三点优势：
- 相较于以前的直接估计参数的方式（这种方式对数据的依赖性较大，相同产生的不同数据可能会给出不同参数）， 加入 random effect 可以使得允许我们研究不同的参照组的结构性联系情况（eg,nested/hirachical），使得我们进行对比观测组更大的 population 的统计推断得以实现。
- 通过 *pooling information* 在不同参照组内取样，能减少数据质量差异带来的误差， 同时也能减少模型的有效参数
- Allow for unobserved factors by including random intercept for individual observations.

假设我们有一个医学实验的数据集，其中Y<sub>i</sub><sub>j</sub>是病人，j=4 病人们被分为4组，每组的用药强度不一样，而我们想研究用药强度和症状的关系。对应的模型如下：
>![image](https://user-images.githubusercontent.com/89850899/159235182-9c371616-4e0d-455e-a6ef-776a0de5bbbf.png)
![image](https://user-images.githubusercontent.com/89850899/159235211-42307d21-922e-4d2f-8436-a8be2cd2abfb.png)

>其中 βj为。fixed effect。β1 = 0 是因为我们假设intercept 代表了一个factor。这样，对于每组的用药强度，我们可以应用一个简单的线性回归函数来得出对应的平均症状严重程度 mu。

可以想到，当各种实验条件/变量在能够得到有效控制/统一的情况下， LM 函数更加方便。 但是现实中很难有这种理想情况，为了尽可能的得到贴近真实情况的推断结果，我们获取的数据也应该尽可能的发散，尽可能的包含所有潜在的因素，而这就导致random effect的引入。 上述例子更多可能发生在药企内部测试中，但当我们进行更高层面的社会实验时，假设我们这次将药品推广到在全市内随机抽取的20个诊所，除了药物本身对病人造成的影响外，结果还可能收到其他random effect的影响， 例如被选中的诊所的治疗对象：一个诊所面对重型糖尿病患者而另一家面对轻微糖尿病，这样同种药物的应用得出的结果也会不同，或者有些诊所的规模更大，应用的药物也就更多，我们得到的数据也就更多更客观 etc，这样，还是套用前面的式子 1-3， 这些random effect 就是gamma， 而当我们搞清楚这random effect 的分布，构成，etc,之后，我们就可以利用这随机抽取的20 个诊所的数据来推断出整个城市的population的情况。 这次的模型中有3个 fixed parameters 即 β0, Y的方差以及random effetct 的方差， 除此之外还有20个ramdon effect,对应我们抽到的20个诊所。
作为对比，下图展示了简单的fixed model 和 random effect model 的对比:
> ![image](https://user-images.githubusercontent.com/89850899/159258976-59faca42-3bb4-4500-a1a1-eeb5b3420753.png)
对于fixed 模型我们需要估计βj，接着对它进行 Hypothesis test 检查他的显著性，对于之前的例子就是检查不同用药强度会不会带来有意义的变化。而对于random effect， 我们要估计的则是rando effect 的方差，再对它进行 Hypothesis test 检测显著性。 对于之前的例子就是说我们要检查不同诊所之间的 random effect 有没有意义。

***Random effect*** 不是一个参数， 但它的 variance 是。

### GLMM in R
混合模型假设：
- response 服从正态分布，相互独立，random effect 对应的conditional variance 应该相等。
- random effect : 服从正态分布， 期望值（mu）为0，而方差不一定要相等
在R中，
GLMM 在R中需要使用 Lme4 package. 在R中，我们可以对模型中的所有参数添加random effect,比较常用的是添加 随机intercept/随机斜率。 Random intercept 可以理解为该组数据在采样时就有偏差，即整组水平要高于/低于其他组别的数据，差别体现在组/level上，而随机斜率则体现在


