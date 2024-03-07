# Pandas notes
some pandas/np notes picked up in work:
- https://www.cnblogs.com/guxh/p/8627251.html 包含所有了基础定位操作
- https://zhuanlan.zhihu.com/p/102274476 图解 pd.merge  基本上来说，合并后的行数要与那边一样，就选那边
- https://mp.weixin.qq.com/s/eFt5-U7F5Fmz7YOqW41ysQ df的各种遍历方法
-     只求满足二分类的df内元素数量：
        df_bool = df['any_col'] == 'any_condition'
        df_bool.sum()  输出每列中符合条件的元素数量
        df_bool.sum（axis= 1） 输出每行符合的数量（一般不用）
        df_bool.values.sum（）输出 df中所有符合的元素的数量（最常用）
        









