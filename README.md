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

par(mar=c(5,4,4,8)+0.1) 
--默认值为mar=c(5,4,4,2)+0.1

plot(x,y,type="b",pch=21,col="red",yaxt="n",lty=3,ann=FALSE)  
--ann(FALSE)用来移除默认标题和坐标轴标签，yaxt="n"和xaxt="n"分别禁用x轴和y轴

lines(x,z,type="b",pch=22,col="blue",lty=2) --添加x对1/x的直线

axis(2,at=x,labels=x,col.axis="red",las=2)  
--绘制坐标轴：2表示在图形那边绘制坐标轴：1=下，2=左，3=上，4=右；at表示需要绘制刻度线的位置；las表示标签是否平行于（=0）或垂直于（=2）坐标轴  

axis(4,at=z,labels=round(z,digits=2),col.axis="blue",las=2,cex.axis=0.7,tck=-.01)  

mtext("y=1/x",side=4,line=3,cex.lab=1,las=2,col="blue")  
--mtext用于在图形边界添加文本

title("An Example of Creative Axes",xlab="X Value",ylab="Y=X")

par(opar)
```
8.参考线
`abline(h=yvalues,v=xvalues)`
- `abline(h=c(1,5,7))`在y为1、5、7位置添加水平实线
- `abline(v=seq(1,10,2),lty=2,col="blue")`在x为1，3，5，7，9的位置添加垂直的蓝色虚线

9.图例
 `legend(location,title,legend,...)`
> 
```
dose<-c(20,30,40,45,60)
drugA<-c(16,20,27,40,60)
drugB<-c(15,18,25,31,40)

opar<-par(no.readonly=TRUE)

par(lwd=2,cex=1.5,font.lab=2)
plot(dose,drugA,type="b",pch=15,lty=1,col="red",ylim=c(0,60),
     main="Drug Dosage",ylab="Drug response")
    
lines(dose,drugB,type="b",pch=17,lty=2,col="blue")

abline(h=c(30),lwd=1.5,lty=2,col="gray")

library(Hmisc)
minor.tick(nx=3,ny=3,tick.ratio=0.5)  --次要刻度线

legend("topleft",inset=.05,title="Drug Type",c("A","B"),
       lty=c(1,2),pch=c(15,17),col=c("red","blue"))
       
```  

10.文本标注,数字标注和图形组合具体代码见书P58-67  


### 第四章 基本数据管理  
1. 创建新变量：使用算数运算符
>
```
mydata<-data.frame(x1=c(2,2,6,4),
                   x2=c(3,4,2,8))
mydata<-transform(mydata,sumx=x1+x2,meanx=(x1+x2)/2) --在原data里面增加数据的和和平均数
```
2.重新编码变量：使用逻辑运算符
>
```
manager<-c(1,2,3,4,5)
data<-c("10/24/14","10/28/14","10/01/14","10/12/14","05/01/14")
country<-c("US","US","UK","UK","UK")
gender<-c("M","F","F","M","F")
age<-c(32,45,25,39,99)
q1<-c(5,3,3,3,2)
q2<-c(4,5,5,3,2)
q3<-c(5,2,5,4,1)
q4<-c(5,5,5,NA,2)
q5<-c(5,5,2,NA,1)
leadership<-data.frame(manager,date,country,gender,age,q1,q2,q3,q4,q5,stringsAsFactors=FALSE) 
--创建leadership数据框

leadership$age[leadership$age==99]<-NA --将年龄为99的重编码为缺失值

leadership$agecat[leadership$age>75]<-"Elder"
leadership$agecat[leadership$age>=55&
                  leadership$age<=75]<-"Middle Age"
leadership$agecat[leadership$age<55]<-"Young" 
--将连续型年龄变量age重编码为类别型变量
或者：
leadership<-within(leadership,{
                   agecat<-NA                            --将每行都设置为缺失值然后依次执行之后的语句
                   agecat[age>75]        <-"Elder"
                   agecat[age>=55&age<=75<-"Middle Age"]
                   agecat[age<55]        <-"Young"})

```
3.更改变量名
`fix(leadership)`

4.缺失值
- 用函数`is.na()`检测缺失值知否存在
>
```
is.na(leadership[,6:10]) --leadership的第六列到第10列
```
- 在分析中排除缺失值
```
x<-c(1,2,NA,3)
y<-sum(x,na.rm=TRUE)
```
- 移除所有含有缺失值的观测
```
newdata<-na.omit(leadership)
```

5.日期
日期的默认输入格式是yyyy-mm-dd
>
```
mydate<-as.Date(c("2017-06-22","2015-09-08"))
```
> 如果用mm/dd/yyyy格式读取数据：
```
strDates<-c("09/30/2019","03/04/2020")
dates<-as.Date(strDates,"%m/%d/%Y")
````
>在leadership中：
```
myformat<-"%m/%d/%y" --y代表两位数年份，Y代表四位数年份
leadership$date<-as.Date(leadership$date,myformat)
```
- tips：`Sys.Date()`可以返回当天日期，`date()`可以返回当前日期和时间  
- 输出指定格式的日期并提取日期值中的某个部分
```
today<-Sys.Date()
format(today,format="%B %d %Y")
format(today,format="%A")
```
- 计算时间
```
startdate<-as.Date("2018-10-22")
enddate<-as.Date("2020-2-3")
days<-enddate-startdate
days
```
> 使用`difftime()`也可计算时间间隔，以星期，天，时，分，秒表示
```
today<-Sys.Date()
dob<-as.Date("1987-3-7")
difftime(today,dob,units="weeks")
```
- 将日期型变量转换为字符型变量
```
strDates<-as.character(dates)
```

6.数据排序
使用`order()`对数据框进行排序，默认升序，在排序变量前加减号可以得到降序结果
```
newdate<-leadership[order(leadership$age)]
```
```
attach(leadership)
newdate<-leadership[order(gender,age),] -- 各行按照女性到男性，同性别中按年龄升序排列
detach(leadership)
```
```
attach(leadership)
newdate<-leadership[order(gender,-age),] --各行按照女性到男性，同性别中按年龄降序排列
detach(leadership)
```

7.数据合并

- 向数据集添加列:`merge()`
```
total<-merge(dataframeA,dataframeB,by="ID")
--将A和B以ID联结：一种inner join

total<-merge(dataframeA,dataframeB.by=c("ID","Country")) --以ID和国家联结

```
> 如果直接横向合并A和B，不需要公共索引：
```
total<-cbind(A,B)
-- A,B 要有同样的行数以同样顺序排列
```
- 纵向合并两个数据，通常用于观测值的添加,A和B要有一样的变量但是顺序不一定相同
```
total<-rbind(A,B)
```
>如果A中有B没有的变量，需要删除A中的多余变量或者在B中创建新的变量并将其设置 为NA

8.取子集
`dataframe[row indices,column indices]`
> `newdata<-leadership[,c[6:10]]`

9.剔除变量
```
myvars<-names(leadership)%in%c("q3","q4")
newdata<-leadership[!myvars]
```
- `names(leadership)`生成了一个包含所有变量名的字符型向量
- `names(leadership)%in%c("q3","q4")`返回了一个逻辑向量：即`name(leadership)`中匹配q3和q4的为TRUE
- ！将逻辑反转即匹配上q3和q4的为FALSE
- `leadership[!myvars]`选择了逻辑值为TRUE的所以q3和q4被剔除

或者在知道q3和q4是第八个和第九个变量的情况下可以使用：
```
newdata<-leadership[c(-8,-9)] --在某列下标之前加（-）会剔除那一列
```
或者可以使用：
```
leadership$q3<-leadership$q4<-NULL
```
10.选入观测
```
newdata<-leadership[1:3,] --选择前三行和所有列

attach(leadership)
newdata<-leadership[gender=="M"&age>30,] 
detach(leadership) 
-- 选择性别男性年龄30岁以上观测值
```
- 选择某个时间范围内的观测值
```
leadership$date<-as.Date(leadership$date,"%m/%d/%y")
startdate<-as.Date("2014-08-10")
enddate<-as.Date("2014-11-01")
newdate<-leadership[which(leadership$date>=startdate&leadership$date<=enddate),]
```
- 使用`subset()`函数
```
newdata<-subset(leadership,age>=35|age<24,select=c(q1,q2,q3,q4))
-- 选择age在35岁以上和24岁一下，保留变量q1到q4
```

```
newdata<-subset(leadership,gender=="M"&age>25,select=gender:q4)
--25岁以上所有男性，保留gender到q4（含）之间的所有列
```

10.随机抽样`sample()`
```
mysample<-leadership[sample(1:nrow(leadership),3,replace=FALSE),]

```
- 1:nrow(leadership)指抽样的pool，这里指leadership里面所有的观测（1-n）
- 3指的是抽取的个数
- replace=FALSE指的是无放回抽样

11.使用SQL语句
```
library(sqldf)
newdf<-sqldf("select * from mtcars where carb=1 order by mpg",row.names=TRUE)
```



























