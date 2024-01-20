---
title: MIT Integration Bee 2023 - Regular Season 部分题目解答
date: 2023-11-25 17:31:32
categories: 
- "MIT Integration Bee"
tags: 微积分
mathjax: enable
---

一些有意思的题的解答，题目见 [这里](https://math.mit.edu/~yyao1/pdf/2023_regular_season.pdf)

## 5.

$$\int_{0}^{\pi/2}x\cot x\mathrm dx$$

**法1：**

$$
\begin{aligned}
\int_{0}^{\pi/2}x\cot x\mathrm dx &= \int_{0}^{\pi/2}x\mathrm d\ln\sin x \\
&= x\ln\sin x\Big |_0^{\pi/2}-\int_0^{\pi/2} \ln \sin x \mathrm dx \\
&= -\int_0^{\pi/2} \ln \sin x \mathrm dx
\end{aligned}
$$

$\ln\sin x$ 在 $[0,\pi/2]$ 上积分是经典的问题。

设

$$I=\int_0^{\pi/2} \ln \sin x \mathrm dx$$

则

$$\int_0^{\pi/2} \ln \cos x \mathrm dx=I$$

$$\int_0^{\pi/2} \ln \sin 2x \mathrm dx=I$$

$$
\begin{aligned}
I&=\int_0^{\pi/2} \ln \sin 2x \mathrm dx \\
&=\int_0^{\pi/2} (\ln 2+\ln\sin x+\ln\cos x) \mathrm dx \\
&= \frac{\pi}{2}\ln 2+2I
\end{aligned}
$$


整理有 $I=-\dfrac{\pi}{2}\ln 2$，故

$$\int_{0}^{\pi/2}x\cot x\mathrm dx=\frac{\pi}{2}\ln 2$$

**法2:**

运用 Feynman 方法，设

$$I(a)=\int_0^{\pi/2}\frac{\arctan(a\tan x)}{\tan x}\mathrm dx$$

所求即 $I(1)$

$$
\begin{aligned}
I^\prime(a)&=\int_0^{\pi/2} \frac{1}{1+a^2\tan^2 x}\mathrm dx \\
&=\int_0^{\pi/2}\frac{1}{(1+a^2\tan^2 x)(1+\tan^2 x)}\cdot \frac{1}{\cos^2 x}\mathrm dx \  (t:=\tan x) \\
&=\int_0^\infty \frac{\mathrm dt}{(1+a^2t^2)(1+t^2)} \\
&=\frac{1}{a^2-1}\int_0^\infty (\frac{a^2}{1+a^2t^2}-\frac{1}{1+t^2})\mathrm dt \\
&=\frac{1}{a+1}\cdot \frac{\pi}{2}
\end{aligned}
$$

同时我们有 $I(0)=0$，因此我们知道

$$I(1)=\int_0^1 I^\prime(a)\mathrm da=\frac{\pi}{2}\ln 2$$

## 8.

$$\int_0^\pi x\sin^4 x\mathrm dx$$

经典方法

$$
\int_0^\pi x\sin^4 x\mathrm dx=\pi \int_0^{\pi/2}\sin^4x\mathrm dx
$$

然后点火，得到 $\dfrac{3}{16}\pi^2$

## 11.

$$\int(\sqrt{2\ln x}+\frac{1}{\sqrt{2\ln x}})\mathrm dx$$

先换元设 $t=\sqrt{\ln x}$

得到

$$\sqrt 2\int (2t^2+1)e^{t^2}\mathrm dt$$

对 $e^{t^2}$ 分部积分

$$\int e^{t^2}\mathrm dt=te^{t^2}-\int 2t^2e^{t^2}\mathrm dt$$

把右边积分挪到左边即得 $(2t^2+1)e^{t^2}$ 的积分，最后得到 $x\sqrt{2\ln x}$

## 13.

$$\int_0^{\frac{\pi}{2}+1}\sin(x-\sin(x-\sin(x-\cdots)))\mathrm dx$$

看到的时候是相当震撼的，实际上不要被他欺骗了。

设 $t=\sin(x-\sin(x-\sin(x-\cdots)))$，则 $t=\sin(x-t)$

两边对 $x$ 求导得到

$$\frac{\mathrm dt}{\mathrm dx}=\sqrt{1-t^2}(1-\frac{\mathrm dt}{\mathrm dx})$$

即

$$\mathrm dx=(1+\frac{1}{\sqrt{1-t^2}})\mathrm dt$$

然后对初始积分做换元，得到

$$\int_0^1 (t+\frac{t}{\sqrt{1-t^2}})\mathrm dt=\frac{3}{2}$$

## 18.

$$\int_0^\infty \frac{x+1}{x+2}\cdot \frac{x+3}{x+4} \cdot \frac{x+5}{x+6} \cdots \mathrm dx$$

设 $A=\dfrac{x+1}{x+2}\cdot \dfrac{x+3}{x+4} \cdots \dfrac{x+2n+1}{x+2n+2}<\dfrac{x+2}{x+3}\cdot \dfrac{x+4}{x+5}\cdots \dfrac{x+2n+2}{x+2n+3}=B$

则 $A<\sqrt{AB}=\sqrt{\dfrac{x+1}{x+2n+3}}$

同理 $A>\dfrac{x+1}{x+2}\cdot \dfrac{x+2}{x+3}\cdot \dfrac{x+4}{x+5}\cdots \dfrac{x+2n}{x+2n+1}=C$

则 $A>\sqrt{AC}=\sqrt{\dfrac{(x+1)^2}{x+2n+1}}$

由极限的夹逼性知，$\lim_{n\to\infty}A=0$，故原积分为 $0$。

## 19.

$$\int_{0}^{\pi/2}\frac{\sin 23x}{\sin x}\mathrm dx$$

经典方法

$$\frac{\sin (2k+1)x}{\sin x}=1+2\sum_{n=1}^k \cos 2nx$$

证明直接数归。

于是直接做完了，积分值为 $\pi/2$。