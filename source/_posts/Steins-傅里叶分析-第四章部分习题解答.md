---
title: Steins 傅里叶分析 第四章部分习题解答
date: 2024-01-09 19:23:41
tags: 傅里叶分析
categories: Steins I
mathjax: enable
---

## Exercise 4

$(\text{Wirtinger} \Rightarrow \text{isoperimetric})$：

$$
\begin{aligned}
2(\pi-\mathcal A)&=\int_{-\pi}^\pi [x^\prime(s)^2+y^\prime(s)^2]\mathrm ds-\int_{-\pi}^\pi [x(s)y^\prime(s)-y(x)x^\prime(s)]\mathrm ds \\
&= \int_{-\pi}^\pi [x^\prime(s)+y(s)]^2\mathrm ds+\int_{-\pi}^\pi[y^\prime(s)^2-y^2(s)]\mathrm ds \\
&\geq 0
\end{aligned}
$$

最后一步利用 Wirtinger 不等式。

$(\text{isoperimetric} \Rightarrow \text{wirtinger})$:

因为 $f$ 连续，所以 $f$ 有原函数，设 $g$ 满足 $g^\prime=-f$

考虑 $\gamma:[-\pi,\pi]\to \mathbb R^2:t\to(g(t),f(t))$

$$
\begin{aligned}
\int_{-\pi}^\pi [f^\prime(t)^2-f^2(t)]\mathrm dt &= \int_{-\pi}^\pi [g^\prime(t)+f(t)]^2\mathrm dt+\int_{-\pi}^\pi [f^\prime(t)^2-f^2(t)]\mathrm dt \\
&=\int_{-\pi}^\pi [g^\prime(t)^2+2g^\prime(t)f(t)+f^\prime(t)^2]\mathrm dt \\
&=\int_{-\pi}^\pi [g^\prime(t)^2+f^\prime(t)^2]\mathrm dt -2\mathcal A \\
&\overset{Cauchy}{\geq} \frac{1}{2\pi} \Bigg(\int_{-\pi}^\pi \sqrt{g^\prime(t)^2+f^\prime(t)^2}\mathrm dt \Bigg)^2-2\mathcal A \\
&=2(\pi-\mathcal A) \\
&\geq 0

\end{aligned}
$$

## Exercise 5

注意到

$$(\frac{1-\sqrt 5}{2})^n+(\frac{\sqrt 5+1}{2})^n$$

是 $a_n=a_{n-1}+a_{n-2},a_1=1,a_2=2$ 的通项公式，而 $(\frac{1-\sqrt 5}{2})^n\to 0$，故随 $n\to\infty$，后面一项无限接近一个整数。

## Exercise 8

$$\Big|\sum_{n=1}^N e^{2\pi ibn^\sigma}\Big|\leq \Big |\sum_{n=1}^Ne^{2\pi ibn^\sigma}-\int_1^N e^{2\pi ibx^\sigma}\mathrm dx\Big|+\Big|\int_1^N e^{2\pi i bx^\sigma}\mathrm dx \Big|$$

而后一项可以利用分部积分提出一个 $e^{2\pi i b x^\sigma}$，证明他是 $O(N^{1-\sigma})$，前一项可以 $(n,n+1)$ 分开考虑放缩，得到 $O(N^\sigma)$，即得证。

## Exercise 9

这次是证明

$$\lim_{N\to\infty}\frac{1}{N}\sum_{n=1}^N e^{2\pi ib\ln n}>0$$

我们还是拆分成 $\sum-\int_1^N$ 和 $\int_1^N$ 两部分，注意到 $\sum-\int_1^N=O(\log n)$，因此不会对极限造成影响，而 $\int_1^N$ 的结果是 $(N^{2\pi ib+1}-1)/(2\pi ib+1)$，由 $|N^{2\pi ib}|=1$ 知最后的极限是 $1/(2\pi i b+1)$

## Exercise 11

首先求出 $u-f$ 的傅里叶系数

$$\widehat{u-f}(n)=\widehat{(f*H_t)}(n)-\widehat f(n)=\widehat f(n)[e^{-4\pi^2n^2t^2}-1]$$

由 Parseval

$$\int_0^1 |u(x,t)-f(x)|^2\mathrm dx=\sum |\hat f(n)|^2+|\widehat{H_t}(n)-1|^2\mathrm dx$$

对于 $\forall \epsilon>0$

注意到因为 $||f||<\infty$，所以存在 $N$ 使得

$$\sum_{|n|>N} |\hat f(n)|<\sqrt \epsilon$$

因此对于 $|n|>N$ 的部分，由 $|\widehat{H_t}(n)-1|\leq 1$ 可知后面的和 $<\epsilon$

对于 $|n|\leq N$ 的部分，我们只需要 $|\widehat{H_t}(n)-1|<\sqrt \epsilon(\forall t<\delta)$ 即可，可取 $\delta=\dfrac{\ln(1-\sqrt \epsilon)}{4\pi^2N^2}$

这样 $\sum=\sum_{|n|\leq N}+\sum_{|n|>N}\leq ||f||\epsilon+\epsilon=O(\epsilon) (t\to 0)$，即证。

## Exercise 13(b)

感觉主要是想到第一步，后面都比较机械了。

先用 Jordan 不等式 $|x|\leq \dfrac{1}{2}|\sin \pi x|,x\in [-\dfrac{1}{2},\dfrac{1}{2}]$，转化成 $\int |\sin\pi xH_t(x)|^2\mathrm dx$，然后 Parseval，转化成傅里叶系数平方求和，用 $\dfrac{1}{2i}(e^{i\pi x}-e^{-i\pi x})$ 代替 $\sin x$，最后可以转化成 $\pi^4t^2\sum |(2n+1)^2e^{-8\pi^2 x^2 t}|$ 的形式，再转换成积分的形式，求阶即可。

## Problem 1

(a) 用 Exercise 15 Chap.3 的结论，有

$$2|a_n|=\frac{1}{2\pi}\int_{-\pi}^\pi (\gamma(t)-\gamma(t+\pi/n))e^{-int}\mathrm dt$$

(b) 设 $t$ 为 $\gamma(\tau)$ 的切线与 $y$ 轴的夹角，则 $\gamma^\prime(t)$ 可写作 $ie^{it}r(t)$，其中 $r(t)$ 控制在 $\tau(t)$ 处的切线长度，则 $r(t)$ 是周期为 $2\pi$ 的实值函数且 $r(t)=-r(t+\pi)$

由分部积分

$$\gamma(t)=r(t)e^{it}-\int r^\prime(t)e^{it}\mathrm dt$$

求傅里叶系数得

$$\hat \gamma(1)=\frac{1}{2\pi}\int_{-\pi}^\pi r(t)\mathrm dt=\frac{1}{2\pi}\int_{-\pi}^\pi|\gamma^\prime(t)|\mathrm dt=\frac{\ell}{2\pi}$$

再由 $2\hat \gamma(1)\leq d$ 即证。

## Problem 3

运用 Problem 2 的结论，数学归纳法，每次差分，直到 $\sigma\in (0,1)$。

## Problem 6

可将 $f(n)$ 拆成若干段单调有界的函数，因此有 $\hat f(n)=O(1/n)$，然后用 Problem 5 的结论。