---
title: 网络流
created: '2020-08-04T09:32:54.780Z'
modified: '2020-08-04T09:34:46.306Z'
---

# 网络流
在一个有向图中，有源点和汇点，每条边上都有一个流量上限。显然，除了源点和汇点，其余点的流入量和流出量应该是相同的（和基尔霍夫定律有点像）。围绕下图展开讲述：

<img align=center>![avatar](/image/image1-1.png)

首先在残余网络初始化时，构建反向边，如下图所示：

<img align=center>![avatar](/image/image1-2.png)

## 符号说明
+ 容量(capacity(e))：表示一条有向边e(u, v)允许的最大的流量。
+ 流量(flow(e))：表示一条有向边e(u, v)总容量中已经被占用的流量。
+ 剩余流量(rest(e))：capacity(e)-flow(e)，表示在某个时刻某条有向边中未被占用的流量。
+ 反向边(reverse)：在构建图时，另外反向构图，边容量初始值为0，以便于撤销原先操作。
+ 层次(level(u))：表示节点u在层次图中与源点的距离，在Dinic算法中会用。

## Ford-Fulkerson算法

首先选取S->16->12->20->T这一条路，可以看出，他们的流量为12，于是残余网络为：

<img align=center>![avatar](/image/image1-3.png)

由图中可以看出，当减去某个值的时候，在其对应的反向图中要加入等量的值，以便于撤销的操作。和电路中一样，当某一条通路中，同时通以I和-I的电流，那么在这张图中，可以看成时无电流。
接着选取S->7->14->7->8->T，残余网络如下图所示;

<img align=center>![avatar](/image/image1-4.png)

源点s只剩下流出量4，选择S->4->10->7->4->T这条路，残余网络如下图所示：

<img align=center>![avatar](/image/image1-5.png)

这时发现源点S没有流出量，遇到终止条件， 此网络的最大流为19+4=23。

至于为什么要加入反向边，看下面一个很简单的例子。
显而易见，这里的最大流是2，分别通过S->1->2->T和S->3->4->T两条路达到。

<img align=center>![avatar](/image/image1-6.png)

但试想在第一次选择增广路的时候，恰巧选择了S->1->4->T，那么残余网络就会变成：

<img align=center>![avatar](/image/image1-7.png)

此时已经达到终止条件，那么最大流就变成了1，与客观事实不符，为了克服这种情况就加入了反向边一说。


——————
今天就写到这吧 orz Adaboost 啥的明天再写吧
