---
title: Steins 傅里叶分析 第二章部分习题解答
date: 2023-12-18 21:22:56
tags: 傅里叶分析
categories: Steins I
mathjax: enable
---

# Exercise

## 9

>定义
>
>$$\chi_{[a,b]}(x)=[x\in[a,b]]$$
>
>(1) 求其在 $[-\pi,pi]$ 上的傅里叶展开
>
>(2) 证明该展开在 $a,b\neq \pi$ 且 $a\neq b$ 时不绝对收敛
>
>(3) 证明该展开在任意一点收敛

(1)，易得

$$f(x)\sim \frac{b-a}{2\pi}+\sum_{n\neq 0}\frac{e^{-ina}-e^{-inb}}{2\pi in}e^{inx}$$

(2)

取 $x=\dfrac{a+b}{2}$，注意到最后是 $\sum \dfrac{\sin n\frac{b-a}{2}}{\pi n}$ 的形式，而 $|\sin \dfrac{b-a}{2}|$ 在大部分地方 $\geq \epsilon >0$，因此不绝对收敛。

(3)

$a=b$ 和 $a=-\pi,b=\pi$ 的情况易证。

$$\hat f(n)e^{inx}+\hat f(-n)e^{-inx}=\frac{\sin n(x-a)-\sin n(x-b)}{\pi n} $$

考虑级数 $\sum \sin n(x-a)-\sin n(x-b)$ 的部分和

$$
\begin{aligned}
\sum_{n=1}^N \sin n(x-a)-\sin n(a-b)&=\frac{\sin \dfrac{N(x-a)}{2}\sin \dfrac{(N+1)(x-a)}{2}}{\sin \dfrac{x-a}{2}}[x\neq a] \\
&- \frac{\sin \dfrac{N(x-b)}{2}\sin \dfrac{(N+1)(x-b)}{2}}{\sin \dfrac{x-b}{2}}[x\neq b] \\
& \leq \frac{1}{\sin \dfrac{x-a}{2}}[x\neq a] + \frac{1}{\sin \dfrac{x-b}{2}}[x\neq b] = O(1)
\end{aligned}
$$


由 A-D 判别法，$\{\dfrac{1}{n\pi}\}_n$ 单调收敛于 0， $\sum \sin n(x-a)+\sin n(x-b)$ 有界，因此 $\sum \hat f(n)e^{inx}+\hat f(-n)e^{-inx}$ 收敛。