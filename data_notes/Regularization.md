# Regularization 正则化
## 1. L2 regularization: Rigid regression(岭回归)
#### 1.1 LR回归回顾
当数据集有足够数据时,最小二乘算法求出的fitted line比较合理,在测试集上测试时也能取得较小的 $R^2$ . 但是过小的训练集样本量会导致拟合出的线在测试集上的 $R^2$
很大,这就是过拟合/high variance(线距离测试集上每个点都很远,但根训练集中的点很近). L2正则通过引入少量bias来减少大量variance从而减少过拟合. 

#### 1.2 Rigid regression 概念
与上面的LR回归相似,在LR中目标是得到最小的 $R^2$ ,  而在 Rigid regression 中,目标则是找到最小的:  
$$R^2 +  \lambda  \times \beta^2 $$

其中 $\lambda$ 是惩罚系数, $\beta^2$ 是回归模型的参数(斜率). 该算法的本质是通过减轻x对y的变化的影响来减少过拟合,e.g. 原来x每增大2,y增加1,在岭回归中因为引入$\beta^2$
就变成现在x增加4,y才增加1. 而这种对y变化的影响亦会随着$\lambda$ 的增大而增大,而fitted line 的斜率也会变得更加平缓.  在多元回归中, 上面的公式则会变为:
$$R^2 +  \lambda  \times \sum\beta^2 $$

岭回归的特点使得它对于那些有许多特征但样本不多的数据,e.g.(100行但有700多列的数据集) 非常有效.
