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




 
