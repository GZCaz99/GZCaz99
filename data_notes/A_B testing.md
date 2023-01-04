 **A/B testing notes**
 
 A/B testing 是一种*hypothesis testing*, 主要用于产品测试, 比如说一家公司中成规模的产品进行迭代时, 对其不同指标要求进行统计推断测试.
 
 > hypothesis test review -- 一种通过统计模型来检查某种factor 对于目标是否显著的方法
 
 A/B testing 的几个步骤:
 
![1672731382981](https://user-images.githubusercontent.com/89850899/210315863-e380230e-9903-4fcd-b6c9-f00da659dc73.png)

其中sample size 的选择很重要, 更多的sample 可以减少 S.E 和 BETA, 从而有更好的 Statictical power(1-Beta). 但是sample 数量的增加也意味着实验过程中各种成本的增加, 所以要注重寻求平衡. 一般来说, 当beta <= 0.2 或者 Statistical power > 0.8 的时候, sample 就足够了.

案例分析: 
一个电商平台主要出售衣物, 此时要对销售情况进行分析. A组提出要在网页上提供相似产品的链接, 因为他们认为顾客可能会倾向于购买与正在购物篮中相似的商品, 该组还认为展示相似产品可以增加零售收入, 但同时也担心是否会使消费者陷入犹豫--他们可能会延迟或者放弃购买. 为了研究是否提供相似商品的展示, A/B test is carried. 下一步就是选择sample, 对于该案例(电商网页)的情况我们有如下几种选样option:
![1672813454422](https://user-images.githubusercontent.com/89850899/210496229-eaf000ce-05d3-4880-bd14-ced7b0dc84b0.png)



