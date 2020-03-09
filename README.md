# R
R in action 
## D1 第一章 
  #### 帮助
`help.start()`  
`help("函数名") or ?函数名`
`example ("函数名")`
  #### 安装包 example
 ```
 help.start()
 install.packages("vcd")  --安装vcd包
 help(package="vcd") 
 library(vcd)
 help(Arthritis) --载入这个包并阅读数据集Arthritis的描述
 Arthrtis  --显示这个数据集的内容
 example(Arthritis)  --运行这个数据集自带的示例
 q()
 
 ```
### 第二章 创建数据集
R拥有很多储存数据的对象类型：标量、向量、矩阵、数组、数据框、列表  
1.向量：储存数值型、字符型或逻辑型数据的 **一维数组**， 用c()创建
> 
``` 
a<-c (1,2,5,3,6,-2)  --数值型
b<-c("one","two","three")  --字符型
c<-c(TRUE,TRUE,TRUE,FALSE,FALSE)  --逻辑型
```
**代码之间不要留空格!**
>定位给定元素特定位置的数值
```
a[3]  --返回：5
a[c(1,3,5)] --返回：1，5，6
a[2:6] --返回的是第二个到第六个数：2，5，3，6，-2
```
> 
```
a<-c(2:6)相当于 a<-c(2,3,4,5,6)
```
 2.矩阵
> 创建矩阵:`matrix()`
```
y<-matrix(1:20,nrow=5,ncol=4)  --创建一个5*4的矩阵
y
cells<-c(1,26,24,68)  --矩阵中的4个cells数字
rnames<-c("R1","R2")
cnames<-c("c1","c2")
mymatrix<-matrix(cells,nrow=2,ncol=2,byrow=TRUE,dimname=list(rnames,cnames)) --cells的数字按行填充为2*2的矩阵
mymatrix
mymatrix<-matrix(cells,nrow=2,ncol=2,byrow=FALSE,dimname=list(rnames,cnames))--cells的数字按列填充2*2的矩阵
mymatrix
```
> X[i,]:矩阵X中的第i行；X[,j]:矩阵X中的第j列；X[i，j]：第i行第j个元素
 

















