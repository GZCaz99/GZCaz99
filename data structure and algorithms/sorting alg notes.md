# Intro 
这篇是关于排序算法的相关笔记

### 常见排序算法
>![1673927378749](https://user-images.githubusercontent.com/89850899/212805854-df4abbe2-e57e-41aa-a04c-9488250fc6f0.png)

要记住他们的平均时间复杂度

#### 选择排序
从上图可以了解, 选择排序是最低效的排序方法. 该方法的基本步骤分为:
- 扫描列表中并记录最小值的index
- 扫描剩余input, 如果有更小的值, 就将它与上一个值的位置对调

该排序算法在python的实现如下:
>![1673943632669](https://user-images.githubusercontent.com/89850899/212845317-bda78c8f-9ff5-472b-93fe-81c6b9efa5b2.png)

值得注意的是该算法中使用了 variable 来储存 index. 这里的i是对列表的每个位置进行循环, 即从第一位到第i-1位, 上图中code也有for i in range 而不是 for i in list  (i/j 在这里都是).
上图的算法是针对升序的需求而写出的, 即当更小的数被扫描到时则将其前移, 针对降序则可以将小于号换成大于号.

