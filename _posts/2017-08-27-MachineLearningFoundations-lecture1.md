---
layout: post
title: '台湾大学林軒田老师的机器学习基石——第一讲'
subtitle: 'the learning problem'
date: 2017-08-27
categories: theoretics
cover: 'http://p2p34wgdt.bkt.clouddn.com/fKPRB'
tags: MachineLearning Mathematics 
mathjax: true
---

# 台湾大学林軒田老师的机器学习基石——第一讲
---
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/fKPRB)

这一讲主要介绍了以下几点内容：
> * Course Introduction
> * What is Machine Learning
> * Applications of Machine Learning
> * Components of Machine Learning
> * Machine Learning and Other Fields

## Course Introduction

![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/obTIz)

> 这一节主要是说明这门课是从基础部分作为切入点包括了从技术和理论等方面的讲解。课程这样设计的目的是因为：
> 1. 如果单从理论上切入则可能会使很多人缺乏兴趣，认为不够实用，但好处是可以从事物的本质去理解这些原理。
> 2. 如果单从技术方面来讲，可能会导致在我们快速的学习了很多的方法之后我们还是对机器学习感到很茫然，不知道从哪些方面入手，不清楚哪些地方适合用哪些方法。

---

>本门课会以讲故事的形式讲述以下四个部分：
> *  When can Machines Learn?(illustrative + technical)
> *  Why can Machines Learn?(theoretical + illustrative)
> *  How can Machine Learn?(technical + practical)
> *  How can Machines Learn Better?(practical + theoretical)


以下是Machine Learning Foundations课程的整体结构:  

| When can machines learn? |  |	
| :--- | :--- |
| Lecture 1	the learning problem: | 
| |	                                1.Course Introduction |
| |	                                2.What is Machine Learning |
| |	                                3.Applications of Machine Learning |
| |		                            4.Components of Machine Learning |
| |		                            5.Machine Learning and Other Fields |
| Lecture 2	learning to answer yes/no: |
| |		                            1.Perceptron Hypothesis Set |
| |		                            2.Perceptron Learning Algorithm (PLA) |
| |		                            3.Guarantee of PLA |
| |		                            4.Non-Separable Data |
| Lecture 3	types of learning: |
| |		                            1.Learning with Different Output Space |
| |		                            2.Learning with Different Data Label |
| |		                            3.Learning with Different Protocol |
| |		                            4.Learning with Different Input Space |
| Lecture 4	feasibility of learning: |
| |		                            1.Learning is Impossible? |
| |		                            2.Probability to the Rescue |
| |		                            3.Connection to Learning |
| |		                            4.Connection to Real Learning |


| Why can machines learn? |  |	
| :--- | :--- |
| Lecture 5	training versus testing: |
| |		                            1.Recap and Preview |
| |		                            2.Effective Number of Lines |
| |		                            3.Effective Number of Hypotheses |
| |		                            4.Break Point |
| Lecture 6	theory of generalization: |
| |	                                1.Restriction of Break Point |
| |	                                2.Bounding Function: Basic Cases |
| |	                                3.Bounding Function: Inductive Cases |
| |	                                4.A Pictorial Proof |
| Lecture 7	the VC dimension: |
| |	                                1.Definition of VC Dimension |
| |	                                2.VC Dimension of Perceptrons |
| |	                                3.Physical Intuition of VC Dimension |
| |	                                4.Interpreting VC Dimension |
| Lecture 8	noise and error: |
| |	                                1.Noise and Probabilistic Target |
| |	                                2.Error Measure |
| |	                                3.Algorithmic Error Measure |
| |	                                4.Weighted Classification |

| How can machines learn? |  |	
| :--- | :--- |
| Lecture 9	linear regression:
| |	                                1.Linear Regression Problem |
| |	                                2.Linear Regression Algorithm |
| |	                                3.Generalization Issue |
| |	                                4.Linear Regression for Binary  Classification |
| Lecture 10	logistic regression: |
| |	                                1.Logistic Regression Problem |
| |	                                2.Logistic Regression Error |
| |	                                3.Gradient of Logistic Regression Error |
| |	                                4.Gradient Descent |
| Lecture 11	linear models for classification: |
| |	                                1.Linear Models for Binary Classification |
| |	                                2.Stochastic Gradient Descent |
| |	                                3.Multiclass via Logistic Regression |
| |	                                4.Multiclass via Binary Classification |
| Lecture 12	nonlinear transformation:
| |	                                1.Quadratic Hypotheses |
| |	                                2.Nonlinear Transform |
| |	                                3.Price of Nonlinear Transform |
| |	                                4.Structured Hypothesis Sets |

| How can machines learn better? |  |
| :--- | :-- |
| Lecture 13	hazard of overfitting:
| |	                                1.What is Overfitting? |
| |	                                2.The Role of Noise and Data Size |
| |	                                3.Deterministic Noise |
| |	                                4.Dealing with Overfitting |
| Lecture 14	regularization: |
| |	                                1.Regularized Hypothesis Set |
| |	                                2.Weight Decay Regularization |
| |	                                3.Regularization and VC Theory |
| |	                                4.General Regularizers |
| Lecture 15	validation: |
| |	                                1.Model Selection Problem |
| |	                                2.Validation |
| |	                                3.Leave-One-Out Cross Validation |
| |	                                4.V-Fold Cross Validation |
| Lecture 16	three learning principles: |
| |	                                1.Occam's Razor |
| |	                                2.Sampling Bias |
| |	                                3.Data Snooping |
| |	                                4.Power of Three |

---
## What is Machine Learning
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/RC9Oy)

我们人的学习是通过从观察中了解事物的特点经过抽象总结后得到的一种**能力(skill)**  
**机器学习**则是通过从数据中抽象出这些数据的特点（规律）后学习到的一种能力(skill)  
这两种学习都是要通过“观察”身边的事物（**数据**），然后**积累经验**，最后才能获得与观察事物有关的能力。

### 那什么是能力呢？
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/fnsLh)

**能力**就是用来改善或是提升某一些表现（performance measure） ，比如说 预测的准确度。
举个简单的例子：
当我们没有学习过算术的时候我们对于算数的准确度会很低，可能会无从下手。但经过我们一点一点的做题训练之后我们逐渐掌握了算数的法则，我们算数的准确度就渐渐的提升上来了，最后我们就掌握了算数这种能力。这就是一种人通过学习获得能力的过程。  
**机器学习**同样如此，机器学习算法通过学习数据中的规律（这些规律是隐藏在数据中，人们不可知的），来逐渐提升对于某件事的表现能力。  
*比如说机器学习在金融领域的应用  
我们有一些金融数据，我们把这些数据喂给机器学习算法后，算法通过学习这些数据中的规律（可能是走势），如果我们通过算法学习到的规律可以使我们收益更高的话我们就说算法学习到了这种能力。*

### 那我们为什么要用机器学习呢？
有人可能会有些疑问，我们为什么要用机器学习算法，我们可以通过自己找规律，然后把这些规则进行编程再让机器做，效果不是很好吗？就像在金融领域我们可以让分析师找出那个规律我们就可以让机器按照找到的规律去预测一样。

我们确实可以人为的找规律，再将这些规律编码到程序中，但是他也是一定的局限性的，特别是在大数据的今天，单靠人从海量的数据中发现隐藏在内的规律绝非易事。

我们再来举个例子：
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/e1ruz)

当我们要写一个识别树的程序的时候，人工的寻找特征就会变得很困难，我们可能要很长的时间才能找到这样一组特征用来识别一棵大树。
回想起我们学会认识树的过程，我们也是通过看了很多树的数据，或者是有其他人告诉我们哪些是树，最后经过我们大脑的学习抽象之后才明白了什么是树。但这种过于抽象的东西我们很难用 **形式化** 的语言来描述。所以我们可以利用机器的运算速度，将这些树的数据喂给机器学习算法，通过算法让机器自己去 **“抽象理解”** 发现树的特征，这样构建的识别程序要比手动查找特征要容易得多。

### 遇到以下几个情况我们可以使用机器学习：
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/KMbm0)

> * 当我们在手动编码一个系统的时候
> > 比如说火星导航，因为我们并没有到过火星，我们并不能告诉计算机怎样走会很安全。我们可以通过机器与环境的互动，来让机器学习到遇到什么问题应该怎么做。
>
> * 当我们不能很容易的用形式化的语言描述一种解决方案的时候
> >例如语音识别和视觉识别
>
> * 当我们需要以人类不能反应的速度快速做决定的时候
> > 例如高频率的交易，我们人不能在30s或者1min内进行多次交易的判断
>
> * 当我们面对大量不同的用户为他们提供个性化服务的时候
> > 例如有针对性的市场营销，或者是个性化推荐

#### 在这些情况下机器学习会比我们人工编码要有优势的多  
*我们也可以将机器学习形象的描述成“Give a computer a fish,you feed it for a day;teach it how to fish, you feed it for a lifetime"——“授人以鱼不如授人以渔”*

### 使用机器学习的三个条件
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/p011F)

> 1. 存在一些“潜在的模式”可以被学习  
即“表现能力”可以被提升，比如在数学，计算的正确率，在金融方面，提高预测的准确度。
> 2. 有解决这样一类问题的规则，但我们不能很容易的形式化的描述出来
所以我们需要用到机器学习
> 3. 是否有包含这种模式（能力）的数据
> 机器学习需要数据去学习  
这三个条件可以作为我们是否要用机器学习的参考

接下来我们来看一道练习：
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/xDv29)

#### 答案解析是:  
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/xwCiN)

> * 第一个选项不能使用机器学习是因为小孩什么时候哭是不确定的，是随机的。  
> * 第二个选项是因为我们可以直接编写程序不需要使用机器学习。  
> * 第四个选项是因为我们没有这方面的数据。

## Application of Machine Learning

机器学习可以应用在来我们的衣食住行以及其他地方
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/zZXDJ)


### 机器学习还可以应用在教育领域
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/WrOIP)
>例如判断学生是否会做对一道题


### 同样也可以用在娱乐方面
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/9hHmA)


> * 如向用户推荐他喜欢的电影


## Components of Machine Learning

接下来我们来看看机器学习的几个要素（以信用卡发放为例）：
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/TtEfn)

> * **input**（输入数据）:x∈X X在这里指的是顾客的申请信息。
> * **output**（输出，想要的结果）：y∈Y 在这里指的是是否发放信用卡这一结果
> * **f:X→Y** 存在的未知的映射关系，是我们期望达到的理想关系
> * **data(training examples,训练样例)**: D={(x_1,y_1 )，(x_2,y_2)，…,(x_N,y_N)},指的是训练数据的集合，每条训练数据都包括一个input和一个output。
> * **Hypinthesis(skill)**:指的是期望算法学习到的一个模型用来掌握某种能力：g:X→Y

#### 接下来我们就来看看他们之间的关系
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/qMvPo)


训练样例集中每一个X→Y的对应关系都是一个未知的目标函数f映射出来的，我们通过将训练样例集送入到机器学习算法A中，希望能够学习到一个函数g能够尽可能的与 f 相似，功能相近。

#### 那这个g长什么样子呢？我们来举个例子
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/BYZah)


H代表的是所有评判是否发信用卡的标准，这里面包含了好的标准和坏的标准，我们要做的就是通过机器学习算法A，从H中挑选最好的一个作为g。  
我们常说的学习模型包括了机器学习算法A和“评判标准”的集合H。

#### 这样一来我们对机器学习的了解就更加全面了
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/rLK59)

机器学习的基本流程：使用data去学习找到最好的映射关系g使他尽可能的接近理想的目标函数f

## Machine Learning and Other Fields
接下来我们来看看机器学习和其他领域的关系，有些同学之前会对这些概念理解的不清楚，下面我们就来看看吧

### 机器学习与数据挖掘
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/ebXkT)


> 数据挖掘指的是从大量数据中找到“有趣”的东西
> * 如果数据挖掘中感兴趣的东西和机器学习中想要“学习”到的东西是一样的，比如预测，那我们就可以认为机器学习和数据挖掘是一样的。
> * 如果机器学习想学习到的“东西”与数据挖掘中感兴趣的“东西”有联系的话，可能机器学习的结果可以更好使数据挖掘找到更感兴趣的“东西”，我们就说他们两个可以互相帮忙
> * 数据挖掘同时还关注在大数据集中的运算效率问题

但总的来说想要区分机器学习和数据挖掘还是挺难的

### 机器学习与人工智能
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/UlnER)


**人工智能**的定义是希望机器能做出一些体现智能的行为，比如说可以聊天，下棋，开车等。
> * 当我们机器学习的目标是实现这些行为的时候，我们就可以用机器学习的工具去实现人工智能。
> * 传统的人工智能可能会编写一系列的规则让机器去判断来体现智能，而我们可以通过机器学习的工具让机器自己去发现这一系列的规则。
机器学习是实现人工智能的一条路径，一种方法。

### 机器学习与统计学
![Untitled Image](http://p2p34wgdt.bkt.clouddn.com/4yTuJ)


**统计学**是使用数据来得出一个我们之前不清楚的结论，像丢硬币的概率
> * 统计学可以作为实现机器学习的一种工具
> * 传统的统计学会过多的关注在数学领域的推论、结论，而很少关心可以怎样通过计算达到我们要的效果。