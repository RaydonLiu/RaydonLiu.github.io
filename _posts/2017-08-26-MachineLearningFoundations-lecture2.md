---
layout: post
title: '台湾大学林軒田老师的机器学习基石——第二讲'
subtitle: 'Learning to Ansower Yes/No'
date: 2017-08-26
categories: theoretics
cover: 'http://p2p34wgdt.bkt.clouddn.com/mhVP9'
tags: MachineLearning Mathematics 
mathjax: true
---

# 台湾大学林軒田老师的机器学习基石——第二讲
这一讲主要讲的是 Learning to Ansower Yes/No
> 总共有四个部分：
> * Perceptron Hypothesis  Set
> * Perceptron Learning Algorithm (PLA)
> * Guarantee of PLA
> * Non-Separable Data

## Perceptron Hypothesis Set
上一讲我们讲了机器学习的大致流程

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/9wQTn)


我们有很多的训练样例**training examples D**（D 是通过一个我们并不知道的函数f求解出来的），我们通过将这个D送入到**learning algorithm A**中，A 通过从 **hypothesis set H**中找到一个适合**D**的一个规则的子集**g**，使得**g**尽可能的接近我们想求的**f**。

这一讲我们讨论的问题是**H**中的哪些规则我们是需要的。

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/UBdG7)

我们继续以上一讲的用户信用评定为例
输入有以下几个特征:  
**age** , **annual salary** , **year in job** , **current debt**  

对于一个输入x，我们计算权重分数，如果这个分数大于某个threshold（阈值）则认为可以发放信用卡，如果这个小于这个threshold我们则认为不能发放信用卡。  
可以发放和不能发放信用卡代表的是两个结果，我们可以分别用+1和-1表示，即+1代表的是可以发放，-1代表的是不能发放。0可以被忽略是因为
$$\sum_{i=1}^d w_ix_i$$  
没有意义，它不能说明这个结果是更倾向于+1还是-1。

> 综上所诉我们可以把这个输入输出的映射设为\\( h(x) \\)
> $$f(x)= \sin \left( \left( \sum_{i=1}^d w_i x_i \right) - threshold \right)$$
> 将\\(x\\)作为输入，\\(h(x)\\)的输出则为\\(\{ +1,-1 \}\\)  

PS：这里的\\(sign\\)表示的是函数\\(sign(x)\\),Wikipedia的解释如下

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/4YkC7)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/BPY5B)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/KMQUF)


我们将这个\\(h(x)\\)称为 **perceptron**(感知器)

我们可以再把\\(h(x)\\)进行简化
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/8lUiA)


在第二个等式中我们将 **(-threshold)** 记作\\(w_0\\)，为了使式子向量化我们需要将X维数也增加1，即令\\(x_0\\)为+1，这样就把 **(-threshold)** 归并到了w中。w与x的维数相较于原来的维数都加了1.
 最后得出
$$h(x)=sign(w^T x)$$
*这是一种向量化形式，w与x是维数相同的向量。*

## Perceptron Learning Algorithm (PLA)
那这个\\(h(x)\\)看起来像什么呢？我们可以举一个**Perception in R2**（二维平面）的例子

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/MHL7z)

这里的顾客特征\\(x\\)(输入）有两维，都位于这个二维平面上  
**labels y**(输出) 有两种结果\\( \{ +1,-1 \}\\)分别用\\('○','╳'\\)表示  
**Hypothesis H** 在这个二维空间代表的是无数条黑色的线( **在更高维空间中他代表的是一个超平面(hyperplanes)** )的集合将正样本与负样本分开。  
所以把这种模型称为 **线性（二进制）** 分类器( **linear(binary)classifiers** )

### 我们有如何从\\(H \\)这个无数条线的集合中选择一条我们需要的呢？

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/E7j1V)


> 我们期望的是想找到一个\\( g\\)尽可能接近我们一直想找到的\\( f \\)  
> 至少是在\\( D \\)这个数据集上，我们可以使得\\( g(x_n)=f(x_n )=y_n \\)  
> 但遇到的问题是在\\( H \\)中我们有无数条线可以选择，我们要选哪一条呢？  
> 有一个办法就是我们可以先随机找一条线\\( (g_0) \\),然后再通过D中的数据修正他，使得在经过多次修正之后能接近我们想要的\\( f \\)
> PS：我们把这个 **\\( g_0 \\)** 记作 **\\( w_0 \\)**

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/8ONUm)

我们使得\\( w_0 \\) 从0开始，然后去修正它。  
对于每次的\\( w_t \\) 的更新，如果发现\\( sign( (w_t)^T x_(n(t))) \\) 在 \\( (x_n(t) ,y_(n(t))) \\)上的结果不等于\\( y_(n(t)) \\) 时，我们就尝试通过以下方法修正这个错误  
$$W_(t+1) \leftarrow  w_t + y_n(t) X_n(t)$$
直到 \\( w_t \\) 在 \\( D \\) 中不发生错误时返回这个\\( w \\)(也称 **\\( w_PLA \\)**)作为我们要找的\\( g \\)
这个方法也可形象的描述成”知错能改“——**A fault confessed is half redressed.**  
>PS:我们可以将这个修正方法形象的描述成向量在几何空间中加法运算，\\( y_n(t) \\) 把握的是修正的方向，是向正样例方向修正还是向负样例方向修正。  
>\\( x_n(t) \\) 表示的是向那个方向修正多少，我们每次修正都会偏向需修正的方向一些。


### 下面我们来举个例子来了解一下这个修正的过程（这里为了可视化效果好，使得\\( x_i \gg x_0 \\)）

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/InI6m)


#### 初始时我们的数据分布是这样的，这时并没有找到一条可以区分这些数据的线


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/pAFB2)


#### 这是第一次修正，紫色线代表的是修正后的方向，因为初始的\\(w_0 \\)  是值全为零的向量，所以\\( w_0 \\) 表示的是一个点。


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/ri9Jt)

#### 这是第二次修正，红色线代表的是当前的权值向量，黑色线代表的是我们需要“偏向”的向量，最后我们就将\\( w_(t) \\) 偏向黑色线一些。  
*PS:我们可以看到整个区域被分割成了两个部分——红色区域和蓝色区域，这两个区域的交界处可以看做是一条线，\\( w_(t) \\) 是这条线的法向量，法向量的方向代表的是这条线分割度两个区域中，正样例的方向。*


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/XXB2A)

#### 这是第三次，我们把一个负样例误以为是正样例，所以我们就向着负样例的反方向进行修正，即\\( w_(t) \\)  要远离\\( x_(t) \\).

### *经过多轮修正*

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/dibXZ)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/fRofe)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/eMFEa)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/bWTvQ)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/ScwVg)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/MouGR)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/ZILdz)


#### 最后我们终于找到了一条线可以完美的将这些数据点都区分开。



## 虽然PLA可以达到我们找这一条分割线的目的，但是还有些问题是值得注意的：

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/gCjOB)


> * PLA什么时候停止，达到没有错误？  
> * 计算的出来的结果可以通用吗？即在这个$D$之外的数据集能不能也能有很好的效果
这个是我们接下来需要了解的

## Guarantee of PLA
我们能找到一条线来区分不同的数据点是因为数据集D本身是线性可分的(**linear sepparable**)


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/49Kmm)


> * 第一幅图我们可以找到一条直线完美的区分两种数据点  
> * 第二幅图我们不可以找到一条完美区分数据点的直线，但是我们可以找到一条能较好区分数据点的直线  
> * 第三幅图我们就完全找不到一条直线来区分这些数据点了

> 接下来我们来证明两个问题：  
> ### 为什么可以通过PLA来找到一个\\( w_t \\)  来尽可能的接近我们想求的\\( w_f \\)?  
> ### 什么时候PLA会停止，即找到那个\\( w_t \\)?


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/6Y4LX)
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/i1w4g)


我们现在就来证明这两个问题：
假设我们的输入\\( D \\)是线性可分的，存在\\( w_f \\) 使得\\( y_n = sign ( (w_f)^T x_n ) \\) , \\( w_0=0 \\)

我们有三个条件:  
> 1、因为\\( w_f  \\)可以很好的分开所有不同的数据点，且不会有点在这条线上，所以\\( y_n w_f^T x_n \\) 表示的是求出点 \\( x_n,y_n) \\)到直线 \\( w_f  \\)的距离，\\( y_n  \\)起到绝对值的作用，则有  
> $$y_n(t) w_f^T x_n(t) \geq \min_{n} y_n w_f^T x_n > 0 \textcircled{1} $$   
> 2、只有在有错误的时候才修正\\( w_t \\)，所以\\( y_n(t) \\) 与 \\( w_t^T x_n(t) \\) 异号，则有  
> $$sign(w_t^T x_n(t)  ) \neq y_n(t) \Leftrightarrow y_n(t)  w_t^T x_n(t) \leq 0 \textcircled{2} $$  
> 3、PLA  
> $$w_t = w_(t-1) + y_n(t-1) x_n(t-1) \textcircled{3} $$ 
  

由③得  
$$
\begin{eqnarray*}
w_f^T w_t & = & w_f^T \left( w_(t−1) +y_n (t−1)  x_n(t−1)  \right) \\
& = & w_f^T w_(t−1)+y_n(t−1)  w_f^T x_n(t−1)\\
& \geq & w_f^T w_(t−1) + \min_{n} y_n(t−1) w_f^T x_n(t−1) \textcircled{4}
\end{eqnarray*} 
$$  

由②③得  
$$
\begin{eqnarray*}
\left \| w_t \right \|^2 & = & \left \| w_(t−1) + y_n(t−1)  x_n(t−1) \right \|^2 \\
& =& \left \| w_(t−1) \right \|^2 + 2 y_n(t−1) w_t^T x_n(t−1) + \left \| y_n(t−1) x_n(t−1) \right \|^2 \\
&\leq& \left \| w_(t−1) \right \|^2 + 0 + \left \| y_n(t−1) x_n(t−1) \right \|^2 \\
&\leq& \left \| w_(t−1) \right \|^2 + \max_{n} \left \| y_n(t−1) x_n(t−1) \right \|^2 \textcircled5
\end{eqnarray*}
$$  
由④经历T次更新得  
$$
\begin{eqnarray*}
w_f^T w_t & \geq & w_f^T w_0 + T\min_{n}y_n w_f^T x_n\\   
w_f^T w_t & \geq & T\min_{n}y_n w_f^T x_n \textcircled6
\end{eqnarray*}
$$  

同理可由⑤得  
$$
\begin{eqnarray*}
\left \| w_t \right \| ^2 & \leq & \left \| w_0 \right \|^2 + T\max_{n} \left \|x_n \right \|^2\\ 
& \leq & T\max_{n} \left \| x_n \right \|^2 \textcircled7
\end{eqnarray*}
$$  

由⑥⑦可得  
$$
\begin{eqnarray*}
\frac {w_f^T} {\left \|w_f \right \|} \frac {w_t} { \left \| w_t \right \|} & \geq & \frac { T \min_{n} y_n w_f^T x_n} { \left \| w_f \right \| \left \| w_t \right \|}\\ 
& \geq & \frac {T\min_{n} y_n w_f^T x_n } { \left \| w_f \right \| \sqrt{T} \max_{n} \left \| x_n \right \|}\\
& \geq & \sqrt{T} \cdot \frac {\min_{n}y_n w_f^T x_n } { \left \| w_f \right \| \max_{n} \left \| x_n \right \| }
\end{eqnarray*}
$$  
$$令constant = \frac {\min_{n} y_n w_f^T x_n } { \left \| w_f \right \| \max_{n} \left \| x_n \right \| }$$  
由夹角余弦公式可知  
$$ \frac {w_f^T} { \left \| w_f \right \|} \frac { w_t } { \left \| w_t \right \| }  \leq 1 $$  
则  
$$
\begin{eqnarray*}
\sqrt{T} \cdot constant & \leq & 1\\
T & \leq & \frac {1} {constant^2}\\ 
& \leq & \frac { ( \left \| w_f \right \| \max_{n} \left \| x_n \right \| )^2} {( \min_{n} y_n w_f^T x_n )^2 } 
\end{eqnarray*}
$$  
$$令 R^2 = \max_{n} \left \| x_n \right \|^2 , \rho = \frac {\min_{n} y_n w_f^T x_n } { \left \| w_f  \right \|} ,则$$
$$ T \leq \frac {R^2} {ρ^2} $$  
由此我们就证明出了**PLA**算法可以修正\\( w_t \\) 接近\\( w_f \\),且**在第\\( T\frac{R^2} {\rho^2} \\)次停止完成搜索**。

## 总结：

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/20KC3)

> * 因为线性可分所以存在\\( w_f \\) 使得\\( w_t \\) 越来越接近他
> * 因为遇到错误会修正所以表明\\( w_t \\) 的长度会缓慢的增长
> * 所以PLA会在找到一个接近\\( w_f \\) 的\\( w_t \\) 时会停下来
> *  **PLA算法的优点是结构简单，代码实现容易。在已知输入数据是线性可分的情况下可以知道什么时候找到\\( w_t \approx w_f \\)**
> * **它的缺点是当我们不知道输入数据是否是线性可分的时候就不清楚PLA什么时候停止。**


## Non-Separable Data
### 输入数据不是线性可分的
#### 输入数据不是线性可分有一种可能是这个数据集有小部分**噪声(noisy)点**，可能由于某些因素使得部分数据与大部分数据之间出现了偏差。但噪声点数据**远少于**正常点数据


![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/tX3vk)


针对这种情况我们可以舍弃掉这些噪声点，找一条能区分最多数据点的线。

### **Pocket Algorithm**就是依照这种思想设计的算法

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/vuBIL)


**Pocket Algorithm** 与**ALP**的不同在于是将\\( w_(t+1) \\) 与\\( \hat {w} \\)进行比较如果\\( w_(t+1) \\) 在整个输入数据集中的效果好则替换。并且也**没有确定的结束时间，需要手动设置迭代次数**。  
Pocket Algorithm虽然可以解决数据集不线性可分问题，当其**比PLA要慢很多**。因为在验证时要遍历整个输入数据集。
