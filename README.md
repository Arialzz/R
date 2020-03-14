# R
R in action 
## 第一章 
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

3.数组 
>
```
dim1<-c("A1","A2")
dim2<-c("B1","B2","B3")
dim3<-c("C1","C2","C3","C4")
z<-array(1:24),c(2,3,4),dimnames=list(dim1,dim2.dim3))  --创建4个2*3的矩阵即一个2*3*4的数组
z
```
3.数组 
>
```
dim1<-c("A1","A2")
dim2<-c("B1","B2","B3")
dim3<-c("C1","C2","C3","C4")
z<-array(1:24),c(2,3,4),dimnames=list(dim1,dim2.dim3))  --创建4个2*3的矩阵即一个2*3*4的数组
z
```

4.数据框：不同的列可以包含不同模式（数据型、字符型等），是一个更一般的矩阵，`data.frame()` 创建
>
```
patientID<-c(1,2,3,4)
age<-c(25,34,29,50)
diabetes<-c("type1","type2","type2","type1")
status<-c("poor","improved","excellent","poor")
patientdata<-data.frame(patientID,age,diabetes,status)
```
>选取其中元素
```
patientdata[1:2]  --第一列和第二列  

patientdata[c("diabetes","status")]  --diabetes和status两列  

patientdata$age  --age一列  

table(patientdata$diabetes,patientdata$status)  --diabetes和status的列联表

```
> case identifier可以通过rname指定
```
patientdata<-data.frame(patientID,age,diabetes,status,row.names=patientID)
```

#### 因子（factor）
变量的分类
- 名义型：类别变量，没有顺序之分,如diabetes
- 有序型：顺序关系而非数量关系，如status
- 连续型：某一个范围内的任意值，同时表示顺序和数量，如age  
名义型和有序型为因子（factor）
`factor()`函数将因子中的类别转化为整数保存
>
```
diabetes<-factor(diabetes)  --内部将其关联为：1=type1，2=type2

status<-factor(status,ordered=TRUE)  --关联1=excellent,2=improved,3=poor

status<-factor(status,ordered=TRUE,levels=c("poor","improved","excellent"))  --指定levels覆盖默认排序

sex<-factor(sex,levels=c(1,2),lables=c("male","female"))

```

> `factor()`的使用
```
patientID<-c(1,2,3,4)
age<-c(25,34,29,50)
diabetes<-c("type1","type2","type2","type1")
status<-c("poor","improved","excellent","poor")
diabetes<-factor(diabetes)
status<-factor(status,ordered=TRUE)
patientdata<-data.frame(patientID,age,diabetes,status)
str(patientdata)  --显示对象结构
summary(patientdata)  --显示对象的统计概要
```

#### 列表（list）  
一些对象的有序集合，可能是若干向量、矩阵、数据框、其他列表的集合
>
```
g<-"my first list"
h<-c(12,14,23,45)
j<-matrix(1:10,nrow=5)
k<-c("one","two","three")
mylist<-list(title=g,ages=h,j,k)  --创建list
mylist
mylist[[2]]  --输出第二个成分相当于 mylist[["ages"]]

```

#### 导入数据  
1.导入excel  
- 将excel数据导出为csv格式  
- 使用`mydataframe<-read.csv(file,opetion)`  
>
```
mydataframe<-read.csv("D:/MyDownloads/tute1.csv,header=TRUE) 
-- header表示文件是否在第一行包含了变量名的逻辑型变量
````  
**注意文件path中的斜杠必须是正斜杠/! 反斜杠\ 会被当作转义符**  

2.导入stata数据  
>
```
library(foreign)
mydataframe<-read.dta("D:/MyDownloads/tute1.dta")
```

### 第三章 图形参数
使用以上导入的数据可以绘制图形
>
```
attach(tu)  --绑定数据框tu
plot(GDP,Sales) --绘制散点图：横轴是GDP，纵轴是Sales
abline(lm(Sales~GDP))  --添加最优拟合曲线（regression）
title("regression of Sales on GDP")  --添加标题
detach(tu)  --解除绑定

```
**在数据框中不要忘记使用attach和detach**  

1. `plot`函数的使用
`plot(x,y,type="b")`   
- 绘制点集（x,y）
- type="b"表示同时绘制点和线  

2.改变图形参数  
- lyt改变线条格式
- pch改变绘制点时的符号
- lyt和pch可以直接添加在plot里面也可以用`par()`函数
>
```
attach(tu)  --绑定数据框tu
par(lyt=2)  --绘制虚线
plot(GDP,Sales，pch=17) --点用三角形表示
abline(lm(Sales~GDP))  --添加最优拟合曲线（regression）
title("regression of Sales on GDP")  --添加标题
detach(tu)  --解除绑定
```  
**`par()`要写在最前面，也可以直接在最前面设定`par(lyt=2,pch=17)`**  

3.颜色
使用颜色下标、颜色名称、十六进制的颜色值、RGB或HSV值来指定颜色
> `col=1`,`col="white"`,`col="#FFFFFF"`  
>`colors()`可以返回所有可用颜色的名称  

4.改变文本属性
指定字号、字体和字样
`par(font.lab=3,cex.lab=1.5,font.main=4,cex.main=2)`  
- `font.lab`:坐标轴标签字体，1=常规，2=粗体，3=斜体，4=粗斜体，5=符号字体  
- `font.main`：标题字体样式  
- `cex.lab`:坐标轴标签缩放倍数，cex默认大小为1，1.5表示放大到默认值的1.5倍  
- `cex.main`:标题的缩放倍数  

5. 图形尺寸和边界尺寸  
- `pin` 英寸表示的图形尺寸（宽和高）  
- `mai`边界大小，单位为英寸，顺序为下左上右  
- `mar`同边界大小，单位为英分
> `par(pin=c(4,3),mai=c(1,.5,1,.2))`

#### Example
>
```
dose<-c(20,30,40,45,60)  
drugA<-c(16,20,27,40,60)  
drugB<-c(15,18,25,31,40)  

opar<-par(no.readonly=TRUE)  --可以修改当前图形  
par(pin=c(2,3))  --设置图形2*3英寸 
par(lwd=2,cex=1.5)  --线条宽度为默认宽度的两倍，符号为默认的1.5倍  
par(cex.axis=.75,font.axis=3)  --坐标轴刻度文本为斜体，默认大小的0.75  
plot(dose,drugA,type="b",pch=19,lty=2,col="red")
plot(dose,drugB,type="b",pch=23,lty=6,col="blue",bg="green")
par(opar)
```  
6.添加文本，自定义坐标轴和图标  
```
plot(dose,drugA,type="b",
     col="red",lty=2,pch=2,lwd=2,
     main="Clinical Trials for Drug A",
     sub="This is hypothetical data",
     xlab="Dosage",ylab="Drug Response",
     xlim=c(0,60),ylim=c(0,70))
```
> 添加标题
```
title(main="My Title",col.main="red",
      sub="My Subtitle",col.sub="blue",
      xlab="My X label",ylab="My Y label",
      col.lab="green",cex.lab=0.75))
```  

7.添加坐标轴  
```
x<-c(1:10)
y<-x
z<-10/x  --生成数据
opar<-par(no.readonly=TRUE)  

par(mar=c(5,4,4,8)+0.1)  --默认值为mar=c(5,4,4,2)+0.1
plot(x,y,type="b",pch=21,col="red",yaxt="n",lty=3,ann=FALSE)  
--ann(FALSE)用来移除默认标题和坐标轴标签，yaxt="n"和xaxt="n"分别禁用x轴和y轴
lines(x,z,type="b",pch=22,col="blue",lty=2) --添加x对1/x的直线

axis(2,at=x,labels=x,col.axis="red",las=2)  
--绘制坐标轴：2表示在图形那边绘制坐标轴：1=下，2=左，3=上，4=右；at表示需要绘制刻度线的位置；las表示标签是否平行于（=0）或垂直于（=2）坐标轴  

axis(4,at=z,labels=round(z,digits=2),col.axis="blue",las=2,cex.axis=0.7,tck=-.01)  

mtext("y=1/x",side=4,line=3,cex.lab=1,las=2,col="blue")  --mtext用于在图形边界添加文本

title("An Example of Creative Axes",xlab="X Value",ylab="Y=X")

par(opar)
```





























































