---
title: MIT Integration Bee 2023 - Semifinal 部分题目解答
date: 2023-12-09 19:36:47
categories: 
- "MIT Integration Bee"
tags: 微积分
mathjax: enable
---
[题目链接](https://math.mit.edu/~yyao1/pdf/2023_semifinal.pdf)

感觉 Semifinal 除了 1.3 和 2.3 神题以外其他的反而比较常规。

## 1.1

$$\int e^{\cos x}\cos(2x+\sin x)\mathrm dx$$

$$
\begin{aligned}
I &=\int e^{\cos x}\cos(x+(x+\sin x))\mathrm dx \\
&= \int e^{\cos x}\Big((1+\cos x)\cos(x+\sin x)-\sin x\sin (x+\sin x)\Big) \mathrm dx-\int e^{\cos x}\cos(x+\sin x)\mathrm dx \\
&= e^{\cos x}\sin(x+\sin x)-\int e^{\cos x}\Big(\cos x\cos\sin x-\sin x\sin\sin x)\mathrm dx \\
&= e^{\cos x}\sin (x+\sin x)-e^{\cos x}\sin\sin x
\end{aligned}
$$

## 1.2

~~不会。~~

直接扔个 [StackExchange](https://math.stackexchange.com/questions/4638248/evaluate-int1-0-9x9-x909x99-x9009x909-x9909x999-x900)

讲真这题神了（

## 1.3

$$\int_0^\pi \frac{1\cos x-\cos 2021x-2\cos 2022 x-\cos 2023 x+2}{1-\cos 2x}\mathrm dx$$

$$
\begin{aligned}
I &=\int_0^\pi \frac{2\cos x+2-(\cos 2021x+\cos 2022 x)-(\cos2022 x-\cos 2023 x)}{1-\cos 2x}\mathrm dx \\
&=\int_0^\pi \frac{2\cos x+2-2\cos\dfrac{x}{2}\Big(\cos\dfrac{4043}{2}x+\cos\dfrac{4045}{2}x\Big)}{1-\cos 2x}\mathrm dx \\
&= \int_0^\pi \frac{2\cos x+2-4\cos^2\dfrac{x}{2}\cos 2022 x}{1-\cos 2x}\mathrm dx \\
&= \int_0^\pi \frac{4\cos^2\dfrac{x}{2}(1-\cos 2022x)}{2\sin^2 x}\mathrm dx \\
&= \int_0^\pi \frac{1-\cos 2022x}{2\cos^2\dfrac{x}{2}}\mathrm dx \\
&= \int_0^\pi \frac{1-\cos 2022x}{1-\cos x}\mathrm dx \\
&= 2022\pi
\end{aligned}
$$

最后一步用了 Fejer 积分：

$$\int_0^{\pi/2}\frac{1-\cos nx}{1-\cos x}\mathrm dx=\frac{n\pi}{2}$$

证明实际上不难：

$$
\begin{aligned}
\frac{1-\cos nx}{1-\cos x} &= \frac{(1-\cos x)+(\cos x-\cos 2x)+\cdots (\cos(n-1)x-\cos nx)}{1-\cos x} \\
&= \frac{2\sin \dfrac{x}{2}\sum_{k=1}^n \sin(k-\dfrac{1}{2})x}{2\sin^2 \dfrac{x}{2}} \\
&=\sum_{k=1}^n \sin(k-\frac{1}{2})x
\end{aligned}
$$

因为

$$
\begin{aligned}
\sin(n+\frac{1}{2})x&=\sin\frac{x}{2}+(\sin \frac{3}{2}x-\sin x)+\cdots+(\sin(n+\frac{1}{2})x-\sin(n-\frac{1}{2})x) \\
&=\sin\frac{x}{2}(1+\sum_{k=1}^n\cos kx)
\end{aligned}
$$


带入上面的式子，得到

$$\frac{1-\cos nx}{1-\cos x}=n+\sum_{k=1}^n\sum_{j=1}^k\cos jx$$

两边在 $(0,\pi)$ 上积分，$\cos kx$ 积分值是 $0$，因此

$$\int_0^\pi \frac{1-\cos nx}{1-\cos x}\mathrm dx=n\pi$$

## 2.2

$$\int_{-2}^2 ((((x^2-2)^2-2)^2-2)^2-2)\mathrm dx$$

找规律，

$$\int_{-2}^2 (x^2-2)\mathrm dx=-\frac{8}{3}$$

$$\int_{-2}^2 ((x^2-2)^2-2)\mathrm dx=-\frac{8}{15}$$

因此原积分 $-\dfrac{8}{255}$

## 2.3

不会。