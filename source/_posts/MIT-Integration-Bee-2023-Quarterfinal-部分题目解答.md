---
title: MIT Integration Bee 2023 - Quarterfinal 部分题目解答
date: 2023-12-04 21:20:48
categories: 
- "MIT Integration Bee"
tags: 微积分
mathjax: enable
---
[题目链接](https://math.mit.edu/~yyao1/pdf/2023_quarterfinal.pdf)

## 2.1

$$\int_{\sqrt e}^\infty x^{-\ln x}\mathrm dx$$

设 $t=\ln x$，积分转化为

$$\int_{1/2}^\infty e^{-t^2+t}\mathrm dt=e^{1/4}\int_{1/2}^\infty e^{(t-1/2)^2}\mathrm dt=e^{1/4}\int_0^\infty e^{-u^2}\mathrm du$$

最后一个积分是经典的结论，这里也证一下。

设 $I=\int_0^\infty e^{-x^2}\mathrm dx$

则

$$I^2=\int_0^\infty\int_0^\infty e^{-x^2-y^2}\mathrm dx\mathrm dy$$

做极坐标换元，

$$\mathrm dx\mathrm dy=\frac{\partial(x,y)}{\partial(r,\theta)}\mathrm dr\mathrm d\theta$$

得到

$$I^2=\int_0^{\pi/2}\mathrm d\theta\int_0^\infty e^{-r^2}r\mathrm dr=\frac{\pi}{4}$$

故 $I=\dfrac{\pi^{1/2}}{2}$，原积分为 $\dfrac{e^{1/4}\pi^{1/2}}{2}$。

## 2.2

$$\int \frac{1-2x}{(1+x)^2x^{2/3}}\mathrm dx$$

做代换 $t= x^{1/3}$，得到

$$I=3\int \frac{1-2t^3}{(1+t^3)^2}\mathrm dt=3\int\frac{1}{1+t^3}-\frac{3t^3}{(1+t^3)^2}\mathrm dt$$

注意到

$$\frac{1}{1+t^3}-\frac{3t^3}{(1+t^3)^2}=\frac{1}{1+t^3}\cdot \frac{\mathrm dt}{\mathrm dt}+t\frac{\mathrm d(\frac{1}{1+t^3})}{\mathrm dt}=\frac{\mathrm d\frac{t}{1+t^3}}{\mathrm dt}$$

故原积分 $I=\dfrac{3x^{1/3}}{1+x}$

## 2.3

$$\lim_{n\to\infty}(\frac{1}{n}\int_0^n \cos^2(\frac{\pi x^2}{\sqrt 2})\mathrm dx)$$

$$I_n=\frac{1}{2}\int_0^n 1+\cos(\sqrt 2\pi x^2)\mathrm dx$$

做代换 $t=x^2$

$$I_n=\frac{n}{2}+\frac{1}{2}\int_0^{\sqrt n}\frac{\cos(\sqrt 2\pi t)}{\sqrt t}\mathrm dt=\frac{n}{2}+O(1)$$

故

$$\lim_{n\to\infty} \frac{1}{n}I_n=\frac{1}{2}$$

上上式最后一步利用了 A-D 判别法，反常积分

$$\int_0^\infty \frac{\cos(\sqrt 2\pi t)}{\sqrt t}\mathrm dt$$

收敛。

## 3.2

$$\int_0^\infty \operatorname{sech}^2(x+\tan x)\mathrm dx$$

首先要用 [Glasser's master theorem](https://en.wikipedia.org/wiki/Glasser%27s_master_theorem)

对于形如 $x-a-\sum_{n=1}^N \dfrac{|a_n|}{x-b_n}$ 的 $u$ 和 $f(x)$，有

$$\text{P.V.}\int_{-\infty}^{+\infty}f(u)\mathrm dx=\text{P.V.}\int_{-\infty}^{+\infty}f(x)\mathrm dx$$

而因为

$$\pi\cot x=\frac{1}{x}+\sum_{i=1}^\infty \Big(\frac{1}{x+i\pi}+\frac{1}{x-i\pi}\Big)$$

做代换 $t=\dfrac{\pi}{2}-x$ 就可以得到 $\tan t$ 的表达式，因此 $x+\tan x$ 是上面 $u$ 的表达形式，所以利用定理，

$$I=\frac{1}{2}\int_{-\infty}^{+\infty}\operatorname{sech}^2x\mathrm dx=\tanh x\Big |_{-\infty}^{+\infty}=1$$