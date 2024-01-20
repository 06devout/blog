---
title: 【CS#1】Set Cover 问题的近似算法
date: 2023-11-12 11:59:27
tags: 近似算法
categories: CS
mathjax: enable
---

## Set Cover

Set Cover 是指给定 $n$ 个元素 $E=\{e_1,\cdots,e_n\}$ 以及 $m$ 个集合 $S_1,\cdots,S_m\subseteq E$，每个集合有代价 $w_1,\cdots,w_m$，要求从这些集合中选出 $k$ 个集合 $S_{i_1},\cdots,S_{i_k}$ 使得 $\cup_{j=1}^k S_{j_k}=E$，且 $\sum_{j=1}^k w_{i_k}$ 最小。

Set Cover 是经典的 NP-complete 问题，同时在近似上也是经典的 LOG-APX-complete 问题。

关于 Set Cover 的 LOG-APX-hard 的证明可以参见 Fiege'98 的论文。

下面我们给出一个 Set Cover 的 $H_n$- 近似。

## $H_n$-Approximation

Set Cover 的近似是非常易于入门的。

我们考虑一个自然的贪心，即每次选择一个“平均代价最小的集合”，把他加到集合中。

具体来说，初始我们选择的集合的集合 $I=\emptyset$，设 $\hat S_k$ 表示 $S_k$ 中现在还没有覆盖的元素的集合，我们每次选择

$$\ell=\operatorname{argmin}_{|\hat S_k|>0} \frac{w_k}{|\hat S_k|}$$

并将他放入 $I$ 中，再从所有 $\hat S_k$ 中去掉 $\ell$，直到我们选出了一个覆盖。

这个过程显然可以在多项式时间内实现，下面我们证明 $\sum_{k\in I}w_k\leq H_n\cdot OPT$.

直觉上来讲，对于一个最优的覆盖 $O$, $\sum_{k\in O}w_k=OPT$，在 $O$ 中一定存在一个集合的平均代价不超过 $OPT/n$，覆盖了第一个之后，相应的，$O$ 中一定存在一个集合平均代价不超过 $OPT/(n-1)$ 来覆盖第二个，以此类推就得到了我们这个算法得到的结果 $\leq OPT\cdot(1+\frac{1}{2}+\cdots+\frac{1}{n})$。

下面是严谨的证明：设加入 $k$ 个集合之后还剩下 $n_k$ 个元素没有被覆盖，则

$$\min_{|\hat S_k|>0}\frac{w_k}{|\hat S_k|}\leq \min_{k\in O \wedge |\hat S_k|>0}\frac{w_k}{|\hat S_k|}$$

根据盐水原理，右边小于等于

$$\frac{\sum_{k\in O\wedge |\hat S_k|>0}w_k}{\sum_{k\in O}|\hat S_k|}\leq \frac{OPT}{n_k}$$

故

$$\sum_{k\in I}w_k\leq \sum_{j=1}^k \frac{n_j-n_{j+1}}{n_j}OPT\leq H_n\cdot OPT$$

即完成了我们的证明。

## Further Application

Set Cover 是（比较少有的） LOG-APX-complete 的问题，所以往往需要证明 LOG-APX-hardness 时往往需要从 Set Cover 来规约。比如 Steiner Tree 等问题的 hardness 可以通过非常简单的规约来解决。

同时这种调和级数的证明方法也可以用在 Steiner Tree Variants 的 $O(\log n)$ Approximation 的正确性的证明。

习题：

对于两个集合 $A,B,A\cap B=\emptyset$，$B$ 中每个元素有代价 $w_k$，对于 $i\in A,j\in B$ 有额外代价 $c_{i,j}$，选取 $B$ 的一个非空子集 $E$，最小化 

$$\sum_{i\in E}w_i+\sum_{i\in A}\min_{j\in E}c_{i,j}$$

通过证明这个问题是 LOG-APX-hard 并给出一个 $O(\log n)$ 近似算法，证明他是 LOG-APX-complete。