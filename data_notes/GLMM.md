# Gneralised Linear Mixed Modles

## Intro
### Random effects
到目前为止，我们讨论的模型参数都是一个未知的固定数值。然而我们也可以将其中的一些参数（e.g: intercept coe, 即b0）视作一个从一个 ‘*secondery distribution*' 中提取的一个随机变量。 这一‘次级分布’限制了参数的取值空间，从而进一步的
‘**Conditionally define**' 了最终的 Respoonse Variable Yi. 这种做法带来的就是***Random effect***。在数学上，对于一个response variable ***Y<sub>i</sub><sub>j</sub>*** ：
  >![image](https://user-images.githubusercontent.com/89850899/159179224-82d7aab3-bac9-4b88-90c9-b4761098dbe9.png)

>其中Y<sub>i</sub><sub>j</sub>是一系列的Response variable, 即共有j组Y，每组中有i个值。例如一个学校有j个班级，每个班级有i个学生。gamma 表示random effect

式子（1）表示***在对应的random effect*** 下，response variable Y<sub>i</sub><sub>j</sub> 服从一个平均数为 mu<sub>j</sub>, 方差为sigma<sub>y</sub><sup>2</sup>的分布(即Y的方差)。式子（2）表示 conditional mean mu<sub>j</sub> 等于 intercept加上 random effect。 式子（3）表示 random effect 服从一个平均数为0，方差为 random effect 方差的正态分布。
