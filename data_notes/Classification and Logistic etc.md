# Clasification
在分类问题中我们需要比较模型对train/test错误率, 对应的自然就有模型的准确率：
> ![image](https://user-images.githubusercontent.com/89850899/161937022-6439f9fc-c58b-4219-ab8f-de9f1a938e79.png)

除此之外， 还有一种常用的方法是建立 confusion matrix:

>![image](https://user-images.githubusercontent.com/89850899/161939551-ffc0253a-fc70-445e-9afd-5e150bfd1f70.png)

上图中的 recall 和 precision 都是衡量模型表现对重要参数， 我们需要找到它们之间的平衡。

## Logistic regression
在分类问题中， 常常设定属于一类的结果为1， 反之则为0， 通过检测对应输入的数据通过分类器计算的对应概率大小来判断它属于/不属于的情况。 此时一个很常用的模型就是逻辑回归， 它能将结果限制在[0,1]这个区间内。
常见形式如下：
>![image](https://user-images.githubusercontent.com/89850899/161987688-bfb61760-f1d7-472c-94e1-1483f212f04c.png)
通常的工作流程则如下：
>![image](https://user-images.githubusercontent.com/89850899/161988007-e6ae3113-0574-4b02-afd8-1d5ffc871744.png)

### Threshold P
分类器通过计算输入数据属于某一类的概率， 当这一概率 P 高于某一 threshold 时， 则判断该数据属于某一类(e.g 当 P threshold > 0.5, x 属于 A类型)。 在建模时，我们可以通过改变 P threshold 来改变模型对应的表现， 尤其是上文提到的准确率平衡。如果我们的首要目标是
正确的对数据进行分类， 那我们可以尝试降低 P threshold 来得到更好的结果。 对应的， 降低了 P threshold会造成耕地的 specificity, 而我们也需要在 specificity 和 sensitivity 达到一个最优的平衡。这种情况下， ROC 可以帮我们更好的做出判断。


### ROC curve
ROC 的定义如下：
>![image](https://user-images.githubusercontent.com/89850899/161991679-fb42af85-65b8-4b6d-b430-cd17f52009d1.png)

ROC 延伸出了另一个分类方法的评估标准 AUC， 它本质上是ROC曲线的面积， 它描述了分类器在所有 P threshold 下的表现。 AUC的评判标准如下：
>![image](https://user-images.githubusercontent.com/89850899/161995492-20e00e03-5dcd-4f46-b91d-0ab82b663d33.png)

AUC 经常被用以衡量不同分类器之间的表现。

### Multiple Logistic regression
![image](https://user-images.githubusercontent.com/89850899/162004173-67539b18-bc7a-4b10-a7d8-9bdbd248ca50.png)

## LDA
逻辑回归直接计算输入数据属于某类class的概率，而另一种没那么直接的方法是将输入数据分入各个class中， 在计算它在这一 class中的概率（在同一class中与其他数据的相似度）， 最后运用贝叶斯理论来获得数据属于某类class的概率， 这样的方法就叫做 Linear discriminant analysis (LDA). 相较于逻辑回归， 当我们有一个较多种类的class时，罗辑回归得到的参数估计在不同class之间会非常不稳定， 而 LDA 就不会受到影响。 此外当数据集较小且输入数据在各个class中大致呈正态分布时， LDA会比罗辑回归更稳定。具体理论如下：
>![image](https://user-images.githubusercontent.com/89850899/162015985-99b9be95-7999-40a4-9c41-883c59f9bb10.png)
π
总的来说， 估计 πk 相对容易，比如对于一个随机trainiing 样本集中我们只需要计算其中 X 属于某类class的比例，e.g 60% X 属于 Y1， 则π1 = 0.6 ...
而估计likelihood则比较困难， 为此LDA做出如下假设， 来帮助我们求得likdelihood:
>![image](https://user-images.githubusercontent.com/89850899/162069490-a61b8279-1b46-45dd-9f45-e57b8f909dca.png)

### 1-dimension LDA
>![image](https://user-images.githubusercontent.com/89850899/162070377-868c7e65-d8e7-4025-a258-e7861b487532.png)
其中δk(x) = log(pk(x))

### LDA extimates
>![image](https://user-images.githubusercontent.com/89850899/162071372-0553cbe1-215c-4db4-9ac9-4fbc822e74c3.png)

在求出各个参数的估计值后，我们得到 LDA 将输入数据分配到某个class中最大的概率：
>![image](https://user-images.githubusercontent.com/89850899/162072259-8473c0ab-e208-469a-ace7-81d9bfbd62fd.png)

### Quadratic discriminant analyisis
QDA 与 LDA最大的不同在于假设class之间的方差不恒定， 即允许了class间方差的变化， 数学表达式如下：
>![image](https://user-images.githubusercontent.com/89850899/162147466-d5e6bc19-dd20-4ce3-9cd5-9d38ea236a47.png)

QDA 在



