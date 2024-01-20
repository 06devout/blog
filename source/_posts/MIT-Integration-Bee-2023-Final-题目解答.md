---
title: MIT Integration Bee 2023 - Final 题目解答
date: 2023-12-12 19:37:15
categories: 
- "MIT Integration Bee"
tags: 微积分
mathjax: enable
---


## 1

$$\int_0^{\pi/2}\frac{\sqrt[3]{\tan x}}{(\cos x+\sin x)^2}\mathrm dx$$

$$
\begin{aligned}
I &= \int_0^{\pi/2}\frac{\sqrt[3]{\tan x}}{(1+\tan x)^2}\mathrm d\tan x \\
&=\int_0^{\infty}\frac{t^{1/3}}{(1+t)^2}\mathrm dt \\
&=\mathcal B(\frac{4}{3},\frac{2}{3}) \\
&=\Gamma(\frac{4}{3})\Gamma(\frac{2}{3}) \\
&=\frac{\Gamma(\dfrac{1}{3})\Gamma(\dfrac{2}{3})}{3} \\
&=\frac{2\pi}{3\sin\dfrac{\pi}{3}} \\
&= \frac{2\sqrt 3}{9}\pi
\end{aligned}
$$

## 2

$$\int_0^\pi \Big(\frac{\sin 2x\sin 3x\sin 5x\sin 30x}{\sin x\sin 6x\sin 10x\sin 15x}\Big)^2\mathrm dx$$

先用二倍角公式上下抵消一下，得到

$$I=\int_0^\pi \Big(\frac{\cos x\cos 15x}{\cos 3x\cos 5x}\Big)^2\mathrm dx$$

然后用三倍角公式展开，得到

$$I=\int_0^\pi\Big(\frac{4\cos^2 5x-3}{4\cos^2 x-3}\Big)\mathrm dx=\int_0^\pi\Big(\frac{2\cos 10x-1}{2\cos 2x-1}\Big)^2\mathrm dx$$

然后做变换 $t=2x$，得到

$$I=\frac{1}{2}\int_0^{2\pi} \Big(\frac{2\cos 5x-1}{2\cos x-1})^2\mathrm dx$$

对这个东西傅里叶展开，得到

$$-1-2\cos x+2\cos 3x+2\cos 4x$$

这个的平方在 $0$ 到 $2\pi$ 积分，因为 $\sin kx$ 是正交的，所以只需要考虑平方的积分，除了常数项是 $2\pi$ 其他的都是 $\pi$，因此

$$I=\frac{1}{2}(2\pi+4\pi+4\pi+4\pi)=7\pi$$

## 3

$$\int_{-1/2}^{1/2}\sqrt{x^2+1+\sqrt{x^4+x^2+1}}\mathrm dx$$

$$
\begin{aligned}
I&=2\int_0^{1/2}\sqrt{\Big(\sqrt{\frac{x^2+x+1}{2}}+\sqrt{\frac{x^2-x+1}{2}}\Big)^2}\mathrm dx \\
&= \sqrt 2\int_0^{1/2}\sqrt{x^2+x+1}\mathrm dx+\sqrt 2\int_0^{1/2}\sqrt {x^2-x+1}\mathrm dx
\end{aligned}$$

后面就是基本的套公式了。

$$I=\frac{\sqrt 7}{2\sqrt 8}+\frac{3}{4\sqrt 2}\ln |\frac{\sqrt 7+2}{\sqrt 3}|$$

## 4

感觉做法挺一眼的，就是可能如果不让用计算器的话最后计算数值解会有些困难？

## 5

$$\int_0^1 \Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}\Big)^2\mathrm dx$$

神仙题呜呜呜

stackexchange 上抄的初等做法。

$$I_a:=\int_0^a \Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}\Big)^2\mathrm dx$$

则对于 $I_1$，我们有两种处理方法，一种是做变换 $t=x/2$，一种是做变换 $t=x-1/2$，这两种都可以得到一个 $I_1$ 和 $I_{1/2}$ 的关系、

首先做变换 $t=x/2$

$$
\begin{aligned}
I_1 &= 2\int_0^{1/2}\Big(\sum_{n=1}^\infty\frac{\lfloor 2^{n+1}x\rfloor}{3^n}\Big)^2 \mathrm dx \\
&= 2\int_0^{1/2}\Big(3\sum_{n=\color{red}1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}\Big)^2 \mathrm dx \\
&= 18 I_1
\end{aligned}
$$

注意红色的地方，本来是没有这一项的，但是因为 $\lfloor 2x\rfloor$ 对于 $x\in (0,1/2)$ 都是 $0$，所以可以添上这一项。

接下来做变换 $t=x-1/2$

$$
\begin{aligned}
I_1 &= \int_0^{1/2}\Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}\Big)^2\mathrm dx+\int_{1/2}^1 \Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}\Big)^2 \mathrm dx \\
&= I_{1/2}+\int_0^{1/2}\Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}-\sum_{n=1}^{\infty}\frac{2^{n-1}}{3^n}\Big)^2 \mathrm dx \\
&= I_{1/2}+\int_0^{1/2}\Big(\sum_{n=1}^\infty\frac{\lfloor 2^nx\rfloor}{3^n}-1\Big)^2\mathrm dx \\
&= 2I_{1/2}+2\int_0^{1/2}\sum_{n=1}^\infty \frac{\lfloor 2^n x\rfloor}{3^n}\mathrm dx+\frac{1}{2}
\end{aligned}
$$


这个一次项的积分是好做的。

$$
\begin{aligned}
\int_0^{1/2}\frac{\lfloor 2^n x\rfloor}{3^n}\mathrm dx &= \frac{1}{6^n}\int_0^{2^{n-1}}\lfloor x \rfloor \mathrm dx \\
&= \frac{1}{6^n}\frac{1}{2}2^{n-1}(2^{n-1}-1) \\
&= \frac{2^{n-1}-1}{4\times 3^n}
\end{aligned}
$$

等比数列求和得到

$$\int_0^{1/2}\sum_{n=1}^\infty \frac{\lfloor 2^n x\rfloor}{3^n}\mathrm dx=\frac{1}{8}$$

带入 $I_{1/2}=I_1/18$，有

$$I_1=\frac{I_1}{9}+\frac{3}{4}$$

整理即得

$$I_1=\frac{27}{32}$$