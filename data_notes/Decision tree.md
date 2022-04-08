# Intro
>![image](https://user-images.githubusercontent.com/89850899/162247364-50e2ab22-5c4d-4ee6-b70a-ae8741c49bfd.png)

原理操作如下：
>![image](https://user-images.githubusercontent.com/89850899/162248201-4585069a-0f90-45b6-8d39-74c1b2dbeef2.png)

术语定义如下：
>![image](https://user-images.githubusercontent.com/89850899/162249483-25780214-d6b6-4db5-85df-fb142a8f673a.png)

## Regression trees
前面介绍了树的结构以及区域划分， 原则上一个区域可以是任何形状，即随着x种类的增加，区域形状可以任意变化， 只要他们不重叠。 对于一个回归树模型，在划分区域时我们需要找到一种划分方法来最小化MSE：
>![image](https://user-images.githubusercontent.com/89850899/162250306-691eba7a-f9ed-4811-bcb0-a950a10e2ad1.png)

