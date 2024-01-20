---
title: Steins 傅里叶分析 第三章部分习题解答
date: 2023-12-29 22:00:56
tags: 傅里叶分析
categories: Steins I
mathjax: enable
---

## Exercise 6

假设存在 $f$ 的傅里叶系数是 $\{a\}$，则 $|f|\leq M$

$$A_r(f)(0)=\bigg|\frac{1}{2\pi}\int_{-\pi}^{\pi}P_r(0-t)f(t)\mathrm dt\bigg|\leq M\frac{1}{2\pi}\int_{-\pi}^\pi P_r(t)\mathrm dt=M$$

另一方面，

$$\bigg|\sum_{n={-\infty}}^\infty a_nr^{|n|}e^{in\theta}\bigg|=\sum_{n=1}^{\infty} \frac{r^n}{n}\to \infty(r\to 1)$$

出现矛盾。

## Exercise 10

$$
\begin{aligned}
E^\prime(t)&=\rho\int_0^{L}\frac{\partial u}{\partial t}\frac{\partial^2 u}{\partial t^2}\mathrm dx+\tau\int_0^L \frac{\partial u}{\partial x}\frac{\partial^2 u}{\partial x\partial t}\mathrm dx \\
&=\rho\int_0^{L}\frac{\partial u}{\partial t}\frac{\partial^2 u}{\partial t^2}\mathrm dx+\tau \frac{\partial u}{\partial t}\frac{\partial u}{\partial x}\Big|_0^L-\tau \int_0^L \frac{\partial u}{\partial t}\frac{\partial^2 u}{\partial x^2}\mathrm dx \\
&=0
\end{aligned}
$$

## Exercise 12

注意到 $\dfrac{1}{\sin \dfrac{x}{2}}-\dfrac{2}{x}$ 在 $0$ 处是可去间断点，补充定义后可令其 $\in \mathcal R[0,\pi]$，由 Riemann-Lebesgue Lemma

$$\int_0^{\pi}\Bigg(\frac{1}{\sin\dfrac{x}{2}}-\frac{2}{x}\bigg)\sin(N+\frac{1}{2})x\mathrm dx\to 0,N\to \infty$$

而 

$$\int_0^\pi \frac{\sin(N+\dfrac{1}{2})x}{\sin \dfrac{x}{2}}\mathrm dx=\int_0^\pi D_N(x)\mathrm dx=\pi$$

得到

$$\int_0^\pi \frac{\sin(N+\dfrac{1}{2})x}{x}\mathrm dx\to \frac{\pi}{2},N\to\infty,N\in \mathbb Z$$

换元得到

$$\int_0^{(N+\frac{1}{2})\pi} \frac{\sin x}{x}\mathrm dx\to \frac{\pi}{2},N\to\infty,N\in \mathbb Z$$

两边取极限即得所求为 $\dfrac{\pi}{2}$

## Exercise 14

$\hat f^\prime(n)=\dfrac{1}{in}\hat f(n)$

于是有

$$\sum_{n\neq 0} |\hat f(n)|\leq \sum_{n\neq 0}\dfrac{|\hat f^\prime(n)|}{|n|}\leq \sqrt{\sum_{n\neq 0}|\hat f^\prime(n)|^2}\cdot\sqrt{\sum_{n\neq 0}\frac{1}{n^2}}=C||f^\prime||< \infty$$

于是 $\sum |\hat f(n)|$ 绝对收敛，即一致收敛。

## Exercise 18

因为 $\epsilon_n\to\infty$，所以 $\forall k\in \mathbb Z^+,\exist \epsilon_{n_k}<\dfrac{1}{2^k}$，取 $f=\sum \epsilon_{n_k}e^{in_kx}$ 即可。

这个练习归纳了之前关于傅里叶级数收敛速度的一些结论。

- $f\in C^k\Rightarrow \hat f(n)=O(1/|n|^k)$
- $f$ is Lipschitz $\Rightarrow \hat f(n)=O(1/|n|)$
- $f$ is monotonic $\Rightarrow \hat f(n)=O(1/|n|)$
- $f$ satisfies Holder's condition with exponent $0<\alpha<1 \Rightarrow \hat f(n)=O(1/|n|^{\alpha})$
- $f$ is Riemann Integrable $\Rightarrow \hat f\in \ell^2,\hat f(n)=o(1)$

## Problem 1

a)

$$\tilde D_N(x)=\frac{\cos\dfrac{x}{2}-\cos(N+\dfrac{1}{2})x}{\sin \dfrac{x}{2}}$$

用和差化积

$$|\tilde D_N(x)|=2\frac{|\sin(\dfrac{N}{2}+1)x\sin Nx|}{|\sin\dfrac{x}{2}|}\leq 2\pi\frac{|\sin Nx|}{|x|}$$

其中用了 $|\sin(\dfrac{N}{2}+1)x| \leq 1$ 和 Jordan 不等式 $|\sin \dfrac{x}{2}|\geq |\dfrac{x}{\pi}|$

对 $\dfrac{|\sin Nx|}{|x|}$ 在 $[0,\pi]$ 上积分，考虑对 $\sin Nx$ 的符号分段讨论，$x$ 放缩成区间左端点，就得到了类似调和级数的表达式，因此为 $O(\log N)$

c)

假设 $\sum_{n=1}^\infty$ 是某个 $f\in\mathcal R$ 的傅里叶级数，则

$$(f*\tilde D_n)(0)=\frac{i}{\pi}\int_0^\pi f(t)\sum_{n=1}^\infty (e^{int}-e^{-int})\mathrm dt=2i\sum_{n=1}^\infty \frac{1}{n^\alpha}=\omega(\log N)$$

得到矛盾，因此不存在这样的 $f$。