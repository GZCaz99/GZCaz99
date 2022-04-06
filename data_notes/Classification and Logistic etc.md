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



