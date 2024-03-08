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
      多个条件之间的情况：
          and : &, or : |, not: ~  ， 其中运算的优先级为 not>and>or
          eg.: df_bool_multi_and = ((df['state'] == 'CA') & (df['age'] < 30))
  
      有时某些列的元素是字符串，这时可以根据这些元素的规律来提取：
            - str.contains（）：包含特定的字符串  e.g:df_str['name'].str.endswith('e')
            - str.endswith（）：以特定字符串结尾
            - str.startswith（）：以特定的字符串开头
            - str.match（）：匹配正则表达式模式
          这些方法只对pd.series生效，也就是说只对df中的列有用，后面可以再接 .sum()查看数量

-         查找缺失值相关：
          # 查找包含缺失值的行
          missing_rows = df[df.isnull().any(axis=1)]
          #查找缺失行的index
          missing_rows.index

-         拼接相关：
              多个df的拼接现在一般用 pd.concat()， 方法中的一些重要参数如下：
              - pd.concat( objs, axis=0, join='outer', join_axes=None, ignore_index=False, keys=None, levels=None, names=None, verify_integrity=False, sort=None, copy=True)
                      - objs 指要合并的df e.g.: pd.concat(df1,df2) ,一般可直接用于拼接两个col一样的df
                      - ignore_index=False ，是否忽视index拼接
                      - verify_integrity ，是否忽视重复index， 当两个df有重复的dx时是否报错
                      - axis ， 一般默认是上下拼接， 单有时也会遇到需要左右拼接的情况，这时候就需要设置 axis = 1
                      - keys/names, 输入合并的df名，这样输出后可以看到拼接后的df中各部分的来源， eg.: pd.concat([df1,df2],names = ['df1','df2'])
      
  


          
        









