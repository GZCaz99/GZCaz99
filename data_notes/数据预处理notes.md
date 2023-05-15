# 机器学习项目的数据处理笔记
在建模前,需要对数据集进行处理,这也是所有学习项目(分类/回归)中最重要且一般耗时最多的部分. 一般来说,每个项目都要求我们根据若干个数据集中提取数据进行建模,常见工作流程如下:
   
   1. 观察数据集,看看是否有重复的特征列,以及各特征列的分布/类型等(EDA阶段)
        - df.head()/df.info()/df.describe()/df.display()..
        - 观察各特征列的类型
        - 观察缺失值情况,选择合适的填充方法或者直接去掉
            - scikitlearn 中的 simple imputer 包
            - xgboost 中自动处理
            - 直接删去(如果占比不多可以考虑,如果某一列的缺失值太多则考虑直接去掉)
            - 异常值(outlier), 观察最大/最小值, 3 $\sigma$ 原则, 箱型图、直方图（尾巴）、散点图（常用）, 方差（离目标远近程度，对噪声敏感）、分位图（0.5%~99.5%）四分位数间距：25%~75%之间的区间宽度。

        - 观察各个特征列中值的分布情况
            - 核密度估计: seaborn.violinplot/histplot...
            - correlation, 热点图
            - 观察label的分布情况: 如果df1中每个x对应一个label, df2中又对应另一个label.../根据项目中不同数据集的特点想办法合并成为一个训练集

        - 数据预处理
            - from sklearn.preprocessing import ...
            - 1. 数据取值范围缩放: 数据标准化（Standardization）用到的多,数据归一化（Scaling）用的少,数据正规化（Normalization）

        
  
  2. 特征工程
     - 特征编码
          - polynomial/label/one-hot/mean encoding ...(特征工程中解释) 
     - 数值型特征:
          - 做对数log变换(train.SalePrice = np.loglp(train.SalePrice)) , 多项式扩展数值特征
            其实就是多项式编码
     - 分类特征:
        - 二值化(binomial),用0/1代表不同类(e.g, iris 是个三分类数据集,但可以)












### 训练集/测试集 合并问题
