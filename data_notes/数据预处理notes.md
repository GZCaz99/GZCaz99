# 机器学习项目的数据处理笔记
在建模前,需要对数据集进行处理,这也是所有学习项目(分类/回归)中最重要且一般耗时最多的部分. 一般来说,每个项目都要求我们根据若干个数据集中提取数据进行建模,常见工作流程如下:
   
   1. 观察数据集,看看是否有重复的特征列,以及各特征列的分布/类型等(EDA阶段)
        - df.head()/df.info()/df.describe()/df.display()..
        - 观察各特征列的类型
        - 观察缺失值情况,选择合适的填充方法或者直接去掉
            - scikitlearn 中的 simple imputer 包
            - LightGBM和XGBoost都能将NaN作为数据的一部分进行学习，所以不需要处理缺失值。
            - 直接删去(如果占比不多可以考虑,如果某一列的缺失值太多则考虑直接去掉)
            - 异常值(outlier), 观察最大/最小值, 3 $\sigma$ 原则, 箱型图、直方图（尾巴）、散点图（常用）, 方差（离目标远近程度，对噪声敏感）、分位图（0.5%~99.5%）四分位数间距：25%~75%之间的区间宽度。

        - 观察各个特征列中值的分布情况
            - 核密度估计: seaborn.violinplot/histplot...
            - correlation, 热点图
            - 观察label的分布情况: 如果df1中每个x对应一个label, df2中又对应另一个label.../根据项目中不同数据集的特点想办法合并成为一个训练集

        - 数据预处理
            - from sklearn.preprocessing import ...
            - 数据取值范围缩放: 数据标准化（Standardization）用到的多,数据归一化（Scaling）用的少,数据正规化（Normalization）
            - Standardization: sklearn.preprocessing.StandardScaler,转换为Z-score，使数值特征列的算数平均为0，方差（以及标准差）为1。不免疫outlier。或者 如果数值特征列中存在数值极大或极小的outlier（通过EDA发现），应该使用更稳健（robust）的统计数据：用中位数而不是算术平均数，用分位数（quantile）而不是方差。这种标准化方法有一个重要的参数：（分位数下限，分位数上限），最好通过EDA的数据可视化确定。免疫outlier。(sklearn.preprocessing.RobustScaler)
            - scaling:将一列的数值，除以这一列的最大绝对值。不免疫outlier。
               -  sklearn.preprocessing.MaxAbsScaler
               -  preprocessing.MinMaxScaler, 将属性缩放到一个指定的最大值和最小值(通常是1-0)之间,对于方差非常小的属性可以增强其稳定性
            - normalization: sklearn.preprocessing.Normalizer
               - 正则化的过程是将每个样本缩放到单位范数(每个样本的范数为1)，如果要使用如二次型(点积)或者其它核方法计算两个样本之间的相似性这个方法会很有用. Normalization主要思想是对每个样本计算其p-范数，然后对该样本中每个元素除以该范数，这样处理的结果是使得每个处理后样本的p-范数(l1-norm,l2-norm)等于1。该方法是文本分类和聚类分析中经常使用的向量空间模型（Vector Space Model)的基础.Normalization主要思想是对每个样本计算其p-范数，然后对该样本中每个元素除以该范数，这样处理的结果是使得每个处理后样本的p-范数(l1-norm,l2-norm)等于1。

        
  
  2. 特征工程
Feature Selection
总的来说，我们应该生成尽量多的 Feature，相信 Model 能够挑出最有用的 Feature。但有时先做一遍 Feature Selection 也能带来一些好处：

Feature 越少，训练越快。
有些 Feature 之间可能存在线性关系，影响 Model 的性能。
通过挑选出最重要的 Feature，可以将它们之间进行各种运算和操作的结果作为新的 Feature，可能带来意外的提高。
Feature Selection 最实用的方法也就是看 Random Forest 训练完以后得到的 Feature Importance 了。其他有一些更复杂的算法在理论上更加 Robust，但是缺乏实用高效的实现，比如这个。从原理上来讲，增加 Random Forest 中树的数量可以在一定程度上加强其对于 Noisy Data 的 Robustness。

看 Feature Importance 对于某些数据经过脱敏处理的比赛尤其重要。这可以免得你浪费大把时间在琢磨一个不重要的变量的意义上。

     - 特征编码
          - polynomial: 它是使用多项式的方法来进行的，如果有a，b两个特征，那么它的2次多项式为（1,a,b,a^2,ab, b^2）https://blog.csdn.net/xiaohutong1991/article/details/107945459
          
     - 数值型特征:
          - 做对数log变换(train.SalePrice = np.loglp(train.SalePrice)) , 多项式扩展数值特征
            其实就是多项式编码
            
     - 分类特征:
        - 二值化(binomial),用0/1代表不同类(e.g, iris 是个三分类数据集,但可以用1来表示第一和第二类,用2来表示第三类), 对于同时属于多类的label,可以参考
        - label encoder, 用有序数据对**不连续**的label 编号, e.g. iris中的花中类, vertosa 设为 3, sentosa 设为 2 ...
        - one-hot encoding, 一般是多类label/类之间没有顺序联系时用, 在数据集中创建一个新的df,有多少类这个数据就有多少维, e.g. 有6类数据, 200行, 维度就是6*200. 
        - meanencoding, 针对高基数类别特征的有监督编码,针对高基数类别特征的有监督编码。当一个类别特征列包括了极多不同类别时（如家庭地址，动辄上万）时，可以采用。优点：和独热编码相比，节省内存、减少算法计算时间、有效增强模型表现。
        - 在类别特征列里，有时会有一些类别，在训练集和测试集中总共只出现一次，例如特别偏僻的郊区地址。此时，保留其原有的自然数编码意义不大，不如将所有频数为1的类别合并到同一个新的类别下(e.g. rare ones)。注意：如果特征列的频数需要被当做一个新的特征加入数据集，请在上述合并之前提取出频数特征。

3. 建立新特征
   特征之间也可以进行操作来合成新特征,可能会产生更好效果:
   - 单独特征列乘以一个常数（constant multiplication）或者加减一个常数：对于创造新的有用特征毫无用处；只能作为对已有特征的处理。
   - 任何针对单独特征列的单调变换（如对数）：不适用于决策树类算法。对于决策树而言https://zhuanlan.zhihu.com/p/26444240
   - 线性组合（linear combination）：仅适用于决策树以及基于决策树的ensemble（如gradient boosting, random forest），因为常见的axis-aligned split function不擅长捕获不同特征之间的相关性；不适用于SVM、线性回归、神经网络等。
   - 比例特征（ratio feature）: 特征1/特质2 = 特征3 ...  绝对值/max/min...
   - 同时利用pandas的groupby操作结合类别与数值特征, e.g.　mean(身高)group_by籍贯...  将这种方法和线性组合等基础特征工程方法结合（仅用于决策树），可以得到更多有意义的特征
   - 提取决策树中生成的向量作为新特征:
      - 在决策树系列的算法中（单棵决策树、gbdt、随机森林），每一个样本都会被映射到决策树的一片叶子上。因此，我们可以把样本经过每一棵决策树映射后的index（自然数）或one-hot-vector（哑编码得到的稀疏矢量）作为一项新的特征，加入到模型中。具体实现：apply()以及decision_path()方法，在scikit-learn和xgboost里都可以用。
   - 树类模型的ensemble: spearman correlation coefficient    /   线性模型、SVM、神经网络: 对数（log）,pearson correlation coefficient

4.Data leakage issues 数据泄露问题
   - https://zhuanlan.zhihu.com/p/26444240










### 训练集/测试集 合并问题
