---
title: 【M#2】 Cesaro 和, Abel 和
date: 2023-12-19 21:01:12
tags: 傅里叶分析
categories: M
mathjax: enable
---

## Cesaro Sum

在考虑一个级数的和的收敛的时候，我们可能会遇到一些问题，比如对于这样一个级数：

$$1,-1,1,-1,1,-1,1,\cdots \tag{1}$$

他的部分和 $s_n=[n \text{ is odd}]$，在常规的意义下他是不可和的，但是他的部分和又表现出了一些收敛的性质。

比如对于这个数列，他的部分和在一半的情况下是 $1$，一半的情况下是 $0$，那么我们把这个和的极限定义为 $1/2$ 是在一定程度上合理的。

所以我们可能需要一些更强的收敛性质。

$\color{red}{定义1}$: 定义

$$\sigma_n=\frac{\sum_{k=0}^{n-1} s_k}{n}$$

为级数 $\{z_n\}$ 的第 $n$ 个 Cesaro 和，其中 $s_n$ 为 $z_n$ 的部分和。

如果 $\sigma_n$ 收敛，则称 $\{z_n\}$ 是 Cesaro 可和的。

在这个定义下，不难验证 $(1)$ 中的 Cesaro 和收敛于 $1/2$。

## Dirichlet Kernal & Fejer Kernel

回忆 Dirichlet Kernel 定义为

$$D_n(x)=\sum_{k=-n}^n e^{inx}=\frac{\sin(n+\dfrac{1}{2})x}{\sin \dfrac{x}{2}}$$

且满足

$$S_n(f)(x)=(f*D_n)(x)$$

我们对于 $f$ 求 Cesaro 和，得到

$$\sigma_n(f)(x)=\frac{S_0(f)(x)+S_1(f)(x)+\cdots+S_{n-1}(f)(x)}{n}=(f*K_n)(f)(x)$$

其中 $K_n$ 为 Fejer Kernel，定义为

$$K_n(x)=\sigma_n(D_n)(x)=\frac{\sin^2 \dfrac{nx}{2}}{n\sin^2\dfrac{x}{2}}$$

注意到 $K_n$ 满足 Good Kernel 的所有性质，这直接得到了 Fejer 定理：

$\color{red}{定理1}$: 如果 $f$ 可积，则 $f$ 的傅里叶级数在每一个 $f$ 的连续点处 Cesaro 可和；进一步的，如果 $f$ 连续，则 $f$ 的傅里叶展开的 Cesaro 和一致收敛与 $f$

## Abel Sum

$\color{red}定义2$: 对于级数 $\{z_n\}$，对于 $0\leq r<1$，定义

$$A(r)=\sum_{k=0}^\infty z_kr^k$$

若 $A(r)$ 收敛，且

$$\lim_{r\to 1}A(r)=s$$

则称 $\{z_n\}$ Abel 可和于 $s$, $s$ 被成为 Abel 均值。

Abel 可和强于 Cesaro 可和，如对于级数

$$1,-2,3,-4,\cdots \tag{2}$$

$$A(r)=\sum_{k=0}^\infty (-1)^k(k+1)r^k=\frac{1}{(1+r)^2}$$

是 Abel 可和的。

但是他不是 Cesaro 可和的，因为

$s_k=\lceil k/2\rceil (-1)^{k+1}$，$s_k$ 的前缀和要么是 $0$ 要么是 $n/2$，他的 Cesaro 部分和要么是 $0$ ，要么是 $1/2$，并不收敛。

## Poisson Kernel

Abel 和对应的 Kernel 是 Poisson Kernel。

对于一个函数 $f(\theta) \sim \sum_n a_ne^{in\theta}$，定义这个函数的 Abel 均值

$$A_r(f)(\theta)=\sum_{n}a_nr^{|n|}e^{in\theta}$$

定义 Poisson Kernel $P_r(\theta)$满足 $A_r(f)(\theta)=(f*P_r)(\theta)$

则

$$P_r(\theta)=\sum_n r^{|n|}e^{in\theta}$$

进一步展开得到

$$P_r(\theta)=\frac{1-r^2}{1-2r\cos\theta+r^2}$$

$P_r(\theta)$ 同样是 Good Kernel，因此将定理1中的 Cesaro 可和结论替换为 Abel 可和结论同样成立。

## Summable & Cesaro Summable & Abel Summable

在本节中，我们将证明三种可和是有强弱关系的，具体来说

$$\text{Summable} \Longrightarrow \text{Cesaro Summable} \Longrightarrow \text{Abel Summable}$$

$\color{red}{定理2}$: 若 $\sum_{k=1}^{\infty} z_k=s$，则 $\{z_n\}$ Cesaro 可和，且 $\sigma=s$

证明是基本的。

在前面已经提到过，存在数列是 Cesaro 可和但不是可和的。

$\color{red}{定理3}$：若 $\{z_n\}$ Cesaro 可和，则 $\{z_n\}$ Abel 可和，且 $\lim_{r\to 1} A(r)=\sigma$

**证明：**

假设 $\sigma=0$，否则可以调整 $z_1$。

$$A(r)=\sum_{n=0}^{\infty}z_nr^n = (1-r)^2\sum_{n=0}^{\infty}n\sigma_nr^n$$

两边在 $r\to 1$ 时取极限，得到 $A(r)\to 0$。

前面同样举出了是 Abel 可和但是不 Cesaro 可和的例子，这完成了单向关系的构建。

## Tauber's Theorem

当然，在对于 $z_n$ 加以额外的限制的情况下，上面三个不同的可和性可以变为等价的。

$\color{red}{定理4}$：若 $z_n$ Cesaro 可和于 $\sigma$，且 $c_n=o(1/n)$，则 $z_n$ 可和于 $\sigma$

**证明：**

$$s_n-\sigma_n=\frac{(n-1)z_n+(n-2)z_{n-1}+\cdots +z_2}{n}$$

两边对 $n$ 取极限。

$\color{red}{定理5}$：若 $z_n$ Abel 可和于 $A$，且 $c_n=o(1/n)$，则 $z_n$ 可和于 $A$

取 $r=1-1/n$

$$
\begin{aligned}
|s_n-\sum_{k=1}^n z_kr^k| &=|\sum_{k=1}^n z_k-\sum_{k=1}^n z_k(1-\frac{1}{n})^k| \\
&\leq |\sum_{k=1}^n z_k(1-(1-\frac{1}{n}))^k| \\
&\leq |\sum_{k=1}^n \frac{kz_k}{n}| +o(1/n) \\
\end{aligned}
$$

对 $n$ 取极限，即证。