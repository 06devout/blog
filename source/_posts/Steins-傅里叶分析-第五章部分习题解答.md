---
title: Steins 傅里叶分析 第五章部分习题解答
date: 2024-01-21 17:19:37
tags: 傅里叶分析
categories: Steins I
mathjax: enable
---

## Exercise 4

(a): 注意到 $f^{(n)}(x)$ 可写作 $P_n(\dfrac{1}{x-a},\dfrac{1}{x-b})e^{-\dfrac{1}{x-a}-\dfrac{1}{x-b}}$，其中 $P_n(s,t)$ 是关于 $s,t$ 的多项式。

我们只需要证明 $f^{(n)}(x)$ 在 $x=a$ 和 $x=b$ 存在即可。

以 $x=a$ 为例，注意到 $x<a,f(x)\equiv 0$，因此 $f^{(n)}(a^-)=0$，同时将 $a^+$ 带入上面那个式子，得到 $f^{(n)}(a^+)=0$，故 $f^{(n)}(a)=0$.

(b): $F(x)=\dfrac{\int_{-\infty}^xf(t)\mathrm dt}{\int_{\mathbb R}f(t)\mathrm dt}$

(c): 

$$g(x)=\begin{cases}
F(\dfrac{(x-a)(b-a)}{\delta}+a)  & \text{ if } x\leq \dfrac{a+b}{2} \\
F(\dfrac{(b-x)(b-a)}{\delta}+a)  & \text{ if } x>\dfrac{a+b}{2}
\end{cases}$$