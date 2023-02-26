# SQL notes

>![image](https://user-images.githubusercontent.com/89850899/221398694-26001965-64d1-4ec3-b826-e91874426fa6.png)
>![image](https://user-images.githubusercontent.com/89850899/221398696-b54784ac-43a1-4089-85db-66c3d10633ad.png)
>![image](https://user-images.githubusercontent.com/89850899/221398703-60461b89-3437-4f6a-8040-0e036f63f923.png)
>![image](https://user-images.githubusercontent.com/89850899/221398722-316a0252-1b6f-4dbf-a038-071647837e89.png)
>![image](https://user-images.githubusercontent.com/89850899/221398728-a931a841-1ac0-4d67-afdd-bc817bb3262e.png)
>![image](https://user-images.githubusercontent.com/89850899/221398735-0a2afd15-bdce-4daf-9a25-0e4f079c4d94.png)



>![1677398097478](https://user-images.githubusercontent.com/89850899/221398888-d58c0a60-d977-4fe8-aa34-a4749b0ccb5c.png)

>对于DECIMAL类,创建时需要输入所谓的 'M' 以及 'D' 的长度, 前者代表创建对象的总长度,,后者代表创建对象的小数部分的长度. e.g: 123.456, M = 6, D = 3


>![1677411583425](https://user-images.githubusercontent.com/89850899/221408280-f83d2175-4fdd-46b7-8dc4-fac5eddc2195.png)

>字符类数据中最常用的就是前两个， 其中定长表示： 不论输入字符有几个字节都是按设定长度，不够的空间就会补足， 例如 char（10） 表示输入一个10字节的字符， 但如果输入字符只有6个， 剩下4个字节就会自动补足到10个， 而varchar相反， 它只限定范围而不限定长度， 例如 varcher（10）只是设定了输入字符的长度上限。 所以在输入字符长度已知并且固定的情况下最好用char（）， 不知道输入字符长度是否固定时用varcahr（）更好

