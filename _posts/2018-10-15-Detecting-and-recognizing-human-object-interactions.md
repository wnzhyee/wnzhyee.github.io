---
layout: post
author: alamoy
title: Paper Reading: Detecting and Recognizing Human-Object Interactions
category: Tech
tag: [paper reading]
---

<script type="text/javascript" src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script>

Kaiming He的一篇CVPR2018，文章地址：[https://arxiv.org/abs/1704.07333](https://arxiv.org/abs/1704.07333)

Task:对一张图像上的<human,action,object>对的检测。即人-动作-物体关系的检测。作者主要在V-COCO和HICO-HET两个数据集上做了实验，模型的性能大概提升了26%，由于基于Faster的模型，所以每张图片135ms，大约7.4FPS。

***
[Q1] “Our human-centric model improves accuracy by 26% (relative) from 31.8 to 40.0 AP...” (Introduction 最后一段第3行)

[A1] **(40.0-31.8)/31.8≈0.26**
***

主要思路：在原Faster上加了两个额外的分支，即一共三个分支(网络图详见文章的Figure 3)

1. Detection Branch: 原Faster上做检测的部分。主要任务仍是检测输入图片的Human和Object的位置

2. Human-centric Branch: 有两个子任务:
  
   第一个是判断框内人的动作(即输入框是人的predict bbox，但做的不是框的检测，而是对框内人的动作作出预测），这个子任务本质上是一个二分类任务，具体来说是对已知的一个动作列表内的每个动作有一个判断是/不是的sigmoid打分(\\(s_h^a\\))。从\\(s_h^a\\)也能看出来，这里只对human-action的关系打分，而不考虑人的动作是否作用到了物体上(这也引出了下一个子任务)。

   第二个子任务即帮上个子任务找出human-antion的目标物体的可能位置。它的输入与之前相同，而输出则是一个用Gauss函数建模的位置分布(\\(g_{h,o}^a\\))。利用文章的公式（2）即可算出object的平均位置(\\(\mu_h^a\\))。

3. Interaction Branch: 与上一个Branch相反，2是用human-action预测object，3则是用human-object预测可能成立的动作。(可以参照Figure7理解一下)。具体操作是通过\\(s_h^a\\)和object的box(\\(b_o\\))算出\\(s_{h,o}^a\\)，输出仍是A维的A个actions的二值sigmoid分类器。

***
[Q2]训练和测试的时候三个分支的输入？

[A2]**训练**的时候并行走，输入都是RPN的输出，Figure3里的b就是所有RPN的输出，\\(b_h\\)则是RPN输出打分后留下的human的pooled feature，\\(b_o\\)类似。(3.1 Model Components中的Object Detection小节的最后一句)

**测试**的时候串行走，先进Detection Branch，再把所有的human和object拿出来再进后面两个Branch，出最终的结果。
***

简单记录下看这篇文章的时候的一些想法和疑惑～

另参考了一些中文博客([1](https://blog.csdn.net/elaine_bao/article/details/80740012),[2](https://blog.csdn.net/qq_37014750/article/details/82469569?utm_source=blogxgwz7),[3](https://blog.csdn.net/sunshine_010/article/details/80036830?utm_source=blogxgwz1)),做下记录，方便之后查阅～感谢前人栽下的树～

2018.10.15
