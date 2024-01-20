---
title: 【M#5】Van der Corput Difference Theorem
date: 2024-01-20 09:00:52
tags: 傅里叶分析
categories: M
mathjax: enable
---

> **Van der Corput Difference Theomrem:** 对于数列 $\{f(n)\}_n$，若 $\forall h\in \mathbb Z$ ,$\{f(n+h)-f(n)\}_n$ 在 $[0,1]$ 上等分布，则 $\{f(n)\}_n$ 在 $[0,1]$ 上等分布。

我们首先证明一个引理：

> **Lemma(Van der Corput's Fundamental Inequality):** 设 $\{u_n\}_{n=1}^N\in\mathbb C,H\in\mathbb Z,1\leq H\leq N$，则有
>
> $$H^2\Bigg|\sum_{n=1}^N u_n\Bigg|^2\leq \color{red}{H(N+H-1)\sum_{n=1}^N |u_n|^2}+\color{green}2(N+H-1)\sum_{h=1}^{H-1}(H-h)\Re\sum_{n=1}^{N-h}u_n\overline{u_{n+h}} \tag{1}$$

证明考虑把 $u_n$ 拓展定义到 $\{u_n\}_n$，其中 $u_k=0,k>N$，那么有

$$H\Bigg|\sum_{n=1}^N u_n\Bigg|=\sum_{p=1}^{N+H-1}\sum_{h=0}^{H-1}u_{p-h}=\sum_{p=1}^{N+H-1}\Bigg(1\cdot \sum_{h=0}^{H-1}u_{p-h}\Bigg)$$

两边用 Cauchy-Schwartz 不等式

$$
\begin{aligned}
H^2\Bigg|\sum_{n=1}^N u_n\Bigg|^2 &\leq (N+H-1)\sum_{p=1}^{N+H-1}\Bigg(\sum_{h=0}^{H-1}u_{p-h}\Bigg)^2 \\
&=(N+H-1)\sum_{p=1}^{N+H-1}\Bigg(\sum_{h_1=0}^{H-1}u_{p-h_1}\Bigg)\Bigg(\sum_{h_2=0}^{H-1}\overline{u_{p-h_2}}\Bigg)
\end{aligned}
$$

对于 $h_1=h_2$ 的单独提出来，就得到了 $(1)$ 中红色的部分

对于 $h_1\neq h_2$ 的部分，考虑 $|h_1-h_2|=h$ 的 $u_n\overline{u_{n+h}}$ 一共出现的次数，以及注意到结果一定是实数，所以虚部抵消掉了，就得到了绿色的部分。

证明了引理之后，我们取 $u_n=e^{2\pi if(n)}$，得到

$$|S_N|^2\leq \frac{H(N+H-1)N}{H^2}+\frac{\sum_{h=1}^{H-1}2(N+H-1)H|\sum_{n=1}^{N-h}e^{2\pi i(f(n+h)-f(n))}|}{H^2}$$

接下来利用放缩 $N+H-1\leq 2N$ 得到

$$
\begin{aligned}
|S_N|^2&\leq \frac{4N}{H}\sum_{h=1}^{H-1}\Bigg|\sum_{n=1}^{N-h}e^{2\pi i(f(n+h)-f(n))}\Bigg| \\
&\leq \frac{4N^2}{H}\sum_{h=1}^{H-1}\Bigg|\frac{1}{N-h}\sum_{n=1}^{N-h}e^{2\pi i(f(n+h)-f(n))}\Bigg|
\end{aligned}
$$

由定理假设，以及 $H$ 为有限数，得后面大 sigma 里面是 $o(1)$，故 $|S_N|^2=o(N^2)$，即证明 $\{f(n)\}$ 是等分布 $[0,1]$ 上的序列。

一些应用：

对于 $\sigma>0,a\neq\in\mathbb Z$,$\{an^\sigma\}$ 在 $[0,1]$ 为等部分序列。

在 Exercise 8 中我们已经证明了 $\sigma\in(0,1)$ 的时候的结果，对于 $\sigma\in (k,k+1)$ 只需要每次差分然后数学归纳即可。