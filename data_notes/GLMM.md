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
