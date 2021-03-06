---
layout: post
title:  机器学习（二十九）——机器学习语录, LightGBM, Parameter Server, LambdaMART
category: ML 
---

# 机器学习语录

这里收录一些网上的只言片语式的心得，以区别于一般的教程。

>首先要考虑你的数据维度是线性相关的还是非线性相关的，数据是稀疏的还是稠密的，正例反例比例是多少，数据量是否充足。数据是否具有可分类性。是否需要降维。是否有噪音，是否有异常点等，然后去选择分类策略。通常包括数据采集，预处理，分类训练，预测，后处理等过程。

## 角度值的特征化

角度值是数据分析中常见的值，然而它不是线性的，比如0度和359度之间只相差1度，然而数值上却差了359度，因此无法将角度值直接代入线性回归等模型。因为后者的loss函数是用线性的欧氏距离定义的，角度显然不满足要求。

既然角度在一维上不是线性的，那么二维呢？没错，可以采用复数坐标(x,y)来表示角度，这样角度就是线性的了。

## 数值计算中的小技巧

1.两个数值趋近于无穷小且相近的数字相除的结果应该大约为1，但却因为分母接近为0而变成无穷。这时可以直接取对数执行运算，其结果在数值上会较为稳定。

## 相关关系不等同于因果关系

我们可以通过一句调侃的话来解释：“地球变暖、地震、龙卷风，以及其他自然灾害，都和18世纪以来全球海盗数量的减少有直接关系”。这两个变量的变化有相关性，但是并不能说存在因果关系，因为往往存在第三类（甚至第4、5类）未被观察到的变量在起作用。相关关系应该看作是潜在的因果关系的一定程度的体现，但需要进一步研究。

# MEMM

Maximum Entropy Markov Model

http://www.cnblogs.com/en-heng/p/6201893.html

中文分词：最大熵马尔可夫模型MEMM

http://www.cnblogs.com/549294286/archive/2013/06/06/3121761.html

统计模型之间的比较，HMM，最大熵模型，CRF条件随机场

http://blog.csdn.net/caohao2008/article/details/4242308

HMM,MEMM,CRF模型的比较

http://blog.csdn.net/zhoubl668/article/details/7787690

标注偏置问题(Label Bias Problem)和HMM、MEMM、CRF模型比较

# CRF

条件随机场(Conditional Random Field)由Lafferty等人于2001年提出，结合了最大熵模型和隐马尔可夫模型的特点，是一种无向图模型，近年来在分词、词性标注和命名实体识别等序列标注任务中取得了很好的效果。

https://mp.weixin.qq.com/s/heYpeVLrZBRjXtMQou2BAA

如何轻松愉快的理解条件随机场（CRF）？

http://www.chokkan.org/software/crfsuite/

CRFsuite: A fast implementation of Conditional Random Fields (CRFs)

https://github.com/scrapinghub/python-crfsuite

A python binding for crfsuite

http://taku910.github.io/crfpp/

CRF++: Yet Another CRF toolkit

# 异常点检测

http://chuansong.me/n/377440751130

异常点检测算法（一）

http://jiangshuxia.9.blog.163.com/blog/static/3487586020083662621887/

异常(Outlier)检测算法综述

http://www.cnblogs.com/fengfenggirl/p/iForest.html

异常检测算法--Isolation Forest

https://mp.weixin.qq.com/s/xsuLIMPJVCThBGMRlz09Hg

Isolation Forest算法原理详解

# 自适应滤波器

《自适应滤波器原理》，Simon Haykin著。

## 基本估计

三种基本的信息处理运算：

**滤波（Filter）**：利用$$[0,t]$$的数据，来估计t时刻信息的运算过程。

**平滑（Smoothing）**：利用$$[0,t]$$的数据，来估计$$t'(t'<t)$$时刻信息的运算过程。

**预测（Prediction）**：利用$$[0,t]$$的数据，来估计$$t+\tau(\tau>0)$$时刻信息的运算过程。

可见，滤波和预测是实时运算，而平滑是非实时运算。

# Robust PCA

http://www.cnblogs.com/quarryman/p/robust_pca.html

最优化之Robust PCA

http://www.aiuxian.com/article/p-2634727.html

Robust PCA

http://blog.csdn.net/abcjennifer/article/details/8572994

Robust PCA学习笔记

http://patternrecognition.cn/~jin/gs/seminar/20140515_jinzhong.ppt

Robust PCA-模式识别

# 热传导推荐算法

https://www.zhihu.com/question/20184666

推荐系统中用到的热传导算法和物质扩散是怎么用的？

http://tis.hrbeu.edu.cn/oa/pdfdow.aspx?Sid=20160307

基于影响力控制的热传导算法

http://www.doc88.com/p-7082821463697.html

改进的热传导和物质扩散混合推荐算法

# 强连通分量算法

http://ishare.iask.sina.com.cn/f/34626295.html

矩阵不可约的充要条件

http://www.cnblogs.com/saltless/archive/2010/11/08/1871430.html

求强连通分量的Tarjan算法

http://blog.csdn.net/dm_vincent/article/details/8554244

求解强连通分量算法之---Kosaraju算法

http://www.cnblogs.com/luweiseu/archive/2012/07/14/2591370.html

强连通分支算法--Kosaraju算法、Tarjan算法和Gabow算法

# Keras

Keras是深度学习的前端框架的集大成者，其后端可支持tensorflow、cntk、theano等。

所谓DL前端框架一般只提供对于DL的高层抽象和封装，至于具体的运算则由具体的后端来实现。

官网：

https://keras.io/

代码：

https://github.com/fchollet/keras/

安装：

`sudo pip install keras`

参考：

https://mp.weixin.qq.com/s/tyWUxJndljOSZT1-aYPgeg

Keras入门必看教程

https://mp.weixin.qq.com/s/57j-YxA4ODMy0RybI8n7uQ

教你在R中使用Keras和TensorFlow构建深度学习模型

https://mp.weixin.qq.com/s/H-oAETObn0SLUxK8--xudg

Keras+OpenAI强化学习实践：行为-评判模型

https://mp.weixin.qq.com/s/2lcOfU3X27YYqbWS341jcg

Keras+OpenAI强化学习实践：深度Q网络

http://mp.weixin.qq.com/s/kvQlzafLAn_8YgBmib3P0g

手把手教你在Amazon EC2上安装Keras

http://www.jianshu.com/p/20585e3b6d02

Keras TensorFlow教程：如何从零开发一个复杂深度学习模型

http://mp.weixin.qq.com/s/sQKhopzS4EOcYwjrM8E7xQ

十分钟搞定Keras序列到序列学习

http://mp.weixin.qq.com/s/F2gBP23LCEF72QDlugbBZQ

详解如何使用Keras实现Wassertein GAN

https://mp.weixin.qq.com/s/PR5gQYEse9KxhSkEVglRWg

用Keras实现seq2seq学习

https://mp.weixin.qq.com/s/0Rdet35LHAXQJuo-r_THXg

如何为LSTM重新构建输入数据（Keras）

https://mp.weixin.qq.com/s/TGjfd3ahYSH_QYX_2j0DqQ

基于Keras的LSTM多变量时间序列预测

https://mp.weixin.qq.com/s/GqaXADRE7Hvxr-6-QapMIg

你必须知道的keras中最常用的深度学习的API

https://mp.weixin.qq.com/s/KE_zk7e6cf5ah303ZTpuMw

如何用Keras为序列预测问题开发复杂的编解码循环神经网络?

https://mp.weixin.qq.com/s/dbZLsWV3pDz3NQPc2aJAUw

用Keras开发字符级神经网络语言模型

https://mp.weixin.qq.com/s/J0pBoNpzj-GYjI-9qefkRg

7步掌握基于Keras的深度学习

https://mp.weixin.qq.com/s/HKOmDltonNpp8DftH7Goww

基于Keras的知识图谱处理实战

https://mp.weixin.qq.com/s/MvEgH-xgNk51qcdlnCJgiQ

Keras教程：用Encoder-Decoder模型自动撰写文本摘要

https://mp.weixin.qq.com/s/ktp4yfxHMt3103QzYhELrg

从头开始在Python中开发深度学习字幕生成模型

https://mp.weixin.qq.com/s/fHuHICI-_xAXIOkV0abpPg

仅需15分钟，使用OpenCV+Keras轻松破解验证码

https://mp.weixin.qq.com/s/I7IUFRVucnJLbGaTqGIXXw

如何使用Keras集成多个卷积网络并实现共同预测

https://mp.weixin.qq.com/s/tW54lcv9aRz9xXC9V-DsWw

Keras+树莓派，130行代码找到圣诞老人

https://mp.weixin.qq.com/s/2jPk3jg7AoNilErAZOaTOQ

输验证码输到崩溃？教你15分钟黑掉全球最流行的验证码插件

# LightGBM

LightGBM是微软推出的boosting框架。

代码：

https://github.com/Microsoft/LightGBM

文档：

https://lightgbm.readthedocs.io/en/latest/

参考：

http://www.msra.cn/zh-cn/news/features/lightgbm-20170105

微软亚洲研究院：LightGBM介绍

https://zhuanlan.zhihu.com/p/25308051

比XGBOOST更快--LightGBM介绍

https://www.zhihu.com/question/51644470

如何看待微软新开源的LightGBM?

http://www.cnblogs.com/rocketfan/p/6005353.html

LightGBM中GBDT的实现

https://zhuanlan.zhihu.com/p/28768447

一个例子读懂LightGBM的模型文件

https://zhuanlan.zhihu.com/p/27916208

LightGBM调参指南(带贝叶斯优化代码)

# CatBoost

这是Yandex推出的Boost工具包。

官网：

https://catboost.yandex/

论文：

《Fighting biases with dynamic boosting》

代码：

https://github.com/catboost/catboost

官方还提供了一个可视化工具：

https://github.com/catboost/catboost-viewer

参考：

https://mp.weixin.qq.com/s/TAminQXid3qq5b8qkeN1rA

ClickHouse如何结合自家的GNDT算法库CatBoost来做机器学习

# Parameter Server

https://www.zhihu.com/question/26998075

最近比较火的parameter server是什么？

http://blog.csdn.net/cyh_24/article/details/50545780

Parameter Server详解

# LambdaMART

https://www.zhihu.com/question/41418093

求解LambdaMART的疑惑？

https://liam0205.me/2016/07/10/a-not-so-simple-introduction-to-lambdamart/

LambdaMART不太简短之介绍

http://blog.csdn.net/huagong_adu/article/details/40710305

Learning To Rank之LambdaMART的前世今生

