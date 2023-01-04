 **A/B testing notes**
 
 A/B testing 是一种*hypothesis testing*, 主要用于产品测试, 比如说一家公司中成规模的产品进行迭代时, 对其不同指标要求进行统计推断测试.
 
 > hypothesis test review -- 一种通过统计模型来检查某种factor 对于目标是否显著的方法
 
 A/B testing 的几个步骤:
 
> ![1672731382981](https://user-images.githubusercontent.com/89850899/210315863-e380230e-9903-4fcd-b6c9-f00da659dc73.png)

其中sample size 的选择很重要, 更多的sample 可以减少 S.E 和 BETA, 从而有更好的 Statictical power(1-Beta). 但是sample 数量的增加也意味着实验过程中各种成本的增加, 所以要注重寻求平衡. 一般来说, 当beta <= 0.2 或者 Statistical power > 0.8 的时候, sample 就足够了.

案例分析: 
一个电商平台主要出售衣物, 此时要对销售情况进行分析. A组提出要在网页上提供相似产品的链接, 因为他们认为顾客可能会倾向于购买与正在购物篮中相似的商品, 该组还认为展示相似产品可以增加零售收入, 但同时也担心是否会使消费者陷入犹豫--他们可能会延迟或者放弃购买. 为了研究是否提供相似商品的展示, A/B test is carried. 下一步就是选择sample, 对于该案例(电商网页)的情况我们有如下几种选样option:
> ![1672813454422](https://user-images.githubusercontent.com/89850899/210496229-eaf000ce-05d3-4880-bd14-ced7b0dc84b0.png)

上图展示了该案例的 customer funnel, 从上到下是不同的用户取样节点,能够获得的样品数量也越来越少. 在第一步也就是当用户登陆进网页时取样, 但在这一节点时我们几乎无法获得任何值得注意的用户特征-- 用户们甚至可能只是手滑了点开网站. 也就是说, 虽然在这一节点时能够获得最多的用户数据, 但是这些数据带来的有价值的特征几乎为0. 一个更有意义的采样节点则是在当消费者开始check out时进行采, 因为在这一阶段顾客已经完成了产品的挑选而且准备结账,因此更能了解产品/消费者的特征/倾向. 这个节点的数据因此在针对分析相似产品投放的时机上最为合适.
准备好取样范围后,下一步就是设计实验. 设计实验的第一个问题则是: *怎样判断指标的有效性?*, 也就是设定一个 Pratical significance boundary. 在本例子中, 设定为当顾客平均消费增加 2$ 时, 则视为投放相似产品的策略是有效的.接着需要设定期望的Statictial power 和 significance level 来计算出需要的样本量, 通常在业界它们分别是80% 和 5%. 计算公式如下:

> ![1672839033466](https://user-images.githubusercontent.com/89850899/210565797-0f782ef6-2334-42c8-b591-cbf620a278dd.png)



