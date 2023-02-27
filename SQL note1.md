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

>![1677490620445](https://user-images.githubusercontent.com/89850899/221527617-6a06a510-6aa2-4a33-9df2-eaf9194693cf.png)

>![1677490723106](https://user-images.githubusercontent.com/89850899/221527995-55996a0e-450f-4249-a3c9-55b5ab2a5c5c.png)

>![1677490746688](https://user-images.githubusercontent.com/89850899/221528080-4bd4860f-312a-43c3-88bb-0b48b79cda16.png)
> ![1677490781959](https://user-images.githubusercontent.com/89850899/221528198-117d0aaf-1d5d-45e9-87d9-504c7ed8f0cc.png)


### DML notes
>![1677490860750](https://user-images.githubusercontent.com/89850899/221528474-51628138-ff5a-43bd-b9d7-a9f37a7abfc2.png)

>![1677490902280](https://user-images.githubusercontent.com/89850899/221528636-61b6becd-6a80-47ab-8596-29cf997f9daf.png)

>![1677490979698](https://user-images.githubusercontent.com/89850899/221528927-90d0c7d4-1809-4e45-a52b-89f538cc2136.png)


### DQL notes

>![1677491413981](https://user-images.githubusercontent.com/89850899/221530626-6732e57f-af51-423f-b2eb-cf4bb73a9c11.png)
>![1677491606134](https://user-images.githubusercontent.com/89850899/221531337-83c4fa17-7727-450c-8a94-19cde0b75464.png)
>![1677491873251](https://user-images.githubusercontent.com/89850899/221532430-5597cc22-ee49-44bb-8ad3-384f28d1352b.png)

>![1677492029679](https://user-images.githubusercontent.com/89850899/221533115-1bd3f441-83f7-450d-8287-afa4cd962a5d.png)
>![1677492341185](https://user-images.githubusercontent.com/89850899/221534337-7e23e671-599c-4138-86fd-b0313ecdef06.png)


>![1677492797369](https://user-images.githubusercontent.com/89850899/221536009-6408b7db-200f-4203-9b50-c1fa0b7fb7ed.png)
>![1677492734036](https://user-images.githubusercontent.com/89850899/221535738-091c06b3-b70c-49e1-bfa1-2e1d9bb4acb4.png)

>![1677493111053](https://user-images.githubusercontent.com/89850899/221537176-924a38ae-07b0-434a-b12f-9f191dd75dc5.png)
>![1677493193535](https://user-images.githubusercontent.com/89850899/221537471-7476a31b-4531-418b-b08e-16be3e9fc4b1.png)

> ![1677494281995](https://user-images.githubusercontent.com/89850899/221541621-cc18bec1-47ad-477e-98d8-f50938255c9c.png)




