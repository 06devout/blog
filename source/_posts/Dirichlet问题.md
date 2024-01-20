---
title: 【M#1】 Dirichlet问题
date: 2023-11-04 19:47:36
tags:
- 微分方程
- 泛函分析
categories: M
mathjax: true
---

# Dirichlet 问题

Dirichlet 问题是指对于实值函数 $V\in C([0,1])$，求常微分方程

$$
(DP)
\left\{\begin{matrix}
-u^{\prime\prime}(x)+V(x)u(x)=f(x)  & x\in [0,1]\\
u(0)=u(1)=0  &
\end{matrix}\right.
$$

的解。

我们接下来会证明，当 $V\geq 0$ 恒成立的时候，$(DP)$ 恒有唯一解。

# 唯一性

**$\color{red}定理1$：** 假设 $V\geq 0$，$f\in C([0,1]),u_1,u_2\in C^2([0,1])$ 是 $(DP)$ 的解，则 $u_1=u_2$

**证明：**

设 $u=u_1-u_2$，则 $u$ 满足

$$\left\{\begin{matrix}
-u^{\prime\prime}+Vu=0  \\
u(0)=u(1)=0
\end{matrix}\right.$$

则

$$
\begin{aligned}
0&=\int_0^1 [-u^{\prime\prime}+Vu]\bar u\mathrm dx \\
&= -\int_0^1 u^{\prime\prime}\bar u\mathrm dx+\int_0^1 V|u|^2\mathrm dx \text{ (分部积分)}\\
&= -u^\prime(x)\bar u(x)\Big |_0^1 +\int_0^1 u^\prime\bar u^\prime\mathrm dx+\int_0^1 V|u|^2\mathrm dx \  (\bar u(0)=\bar u(1)=0) \\
&= \int_0^1 |u^\prime|^2\mathrm dx+\int_0^1 V|u|^2\mathrm dx\geq \int_0^1 |u^\prime|\mathrm dx
\end{aligned}
$$

所以 $u^\prime =0,u$ 为常函数， $u=u(0)=0$.

# $V=0$ 的情况

我们先考虑 $V=0$.

**$\color{red}定理2$：** 定义

$$
K(x,y)=\left\{\begin{matrix}
(x-1)y & 0\leq y\leq x\leq 1 \\
(y-1)x & 0\leq x\leq y\leq 1
\end{matrix}\right.
\in C([0,1]\times [0,1])
$$

并定义运算 $A$： 

$$Af(x)=\int_0^1 K(x,y)f(y)\mathrm dy$$

则 $A\in\mathcal B(L^2([0,1]))$ 为 compact symmetric 算子，且对于 $f\in C([0,1]),Af$ 是常微分方程

$$
\left\{\begin{matrix}
-u^{\prime\prime}(x)=f(x)  & x\in [0,1]\\
u(0)=u(1)=0  &
\end{matrix}\right.
$$

的唯一解。

**注：实际上在下面的证明过程中，我们并不依赖 $K(x,y)$ 具体是多少，定理成立只需要 $K(x,y)$ 有界实值即可，但这里明确给出 $K$ 是因为这个就是解决 Dirichlet 问题的 Kernel。**

**证明：**

先证 $A$ 是紧(compact)的：设 $C=\sup_{[0,1]\times [0,1]} K(x,y)$

$$
\begin{aligned}
|Af(x)| &= |\int_0^1 K(x,y) f(y)\mathrm dy| \\
&\leq C\int_0^1 |f(y)|\mathrm dy (\text{ Cauchy-Schwarz 不等式}) \\
&\leq C(\int_0^1 1^2)^{1/2}(\int_0^1 |f(y)|^2 \mathrm dy)^{1/2} \\
&= C ||f||_2
\end{aligned}
$$

即 $Af$ 一致有界，同理对于 $\forall x,z$ 有

$$|Af(x)-Af(z)|\leq \sup_{y\in [0,1]} |K(x,y)-K(z,y)|\cdot ||f||_2$$

故 $Af$ 是连续的

有了这两个性质，运用 [Arzela-Ascoli Theorem](https://en.wikipedia.org/wiki/Arzel%C3%A0%E2%80%93Ascoli_theorem) 就可以证明 $A$ 是紧的。

接下来证明 $A$ 是对称(symmetric)的

$$
\begin{aligned}
\langle Af,g \rangle_2 &= \int_0^1 \Big[ \int_0^1 K(x,y)f(y)\mathrm dy\Big] \overline{g(x)}\mathrm dx (\text{ 交换积分次序}) \\
&= \int_0^1 f(y) \overline{\Big[\int_0^1 \overline{K(x,y)} g(x)\mathrm dx \Big]}\mathrm dy \\
&= \int_0^1 f(y) \overline{\Big[\int_0^1 K(x,y) g(x)\mathrm dx \Big]}\mathrm dy \\
&= \langle f,Ag \rangle_2
\end{aligned}
$$

故 $A$ 是对称的。

不难验证 $u=Af$ 确实是函数的一个解。

# $V\neq 0$ 的情况

首先给出一个 sketch。

问题等价于求解 $-u^{\prime\prime}=f-Vu$，即求 $u=A(f-Vu)$，即求 $(I+Av)u=Af$.

把 $u$ 写作 $u=A^{1/2}v$，注意我们这里只是一个 sketch，我们接下来会证明 $A^{1/2}$ 存在且为紧且对称的（说明他有逆）

则原来的问题转化成

$$A^{1/2}(I+A^{1/2}VA^{1/2})v=Af$$

即

$$(I+A^{1/2}VA^{1/2})v=A^{1/2}f$$

我们接下来要做的就是证明 $A^{1/2}$ 是存在的，但这还不足以说明问题，因为我们还需要求出 $v$，这需要 $(I+A^{1/2}VA^{1/2})$ 是可逆的，

**$\color{red}引理3$：** $NULL(A)=\{0\}$，且 $A$ 存在一组无穷特征值 $\{\lambda_k\}_k$ 即其对应的正交单位特征向量 $\{u_k\}_k$ 满足

$$\left\{\begin{matrix}
u_k(x)=\sqrt 2\sin 2k\pi x  & \\
\lambda_k=\dfrac{1}{k^2\pi^2} &
\end{matrix}\right. \forall k\in\mathbb N$$

**证明：**

因为 $NULL(A)=\overline{Range(A)}^\bot$，只需证明 $\overline{Range(A)}=L^2([0,1])$ 即可。

取 $u$ 为 $[0,1]$ 上的多项式，取 $f=-u^{\prime\prime}$，此时 $Af=0$ 是唯一的 $(DP)$ 的解，故 $Range(A)$ 包含所有的 $[0,1]$ 上的多项式。

因为 $[0,1]$ 上的多项式是致密的，且任意一个连续函数可以用多项式来逼近 ([Weierstrass Approximation Theorem](https://en.wikipedia.org/wiki/Stone%E2%80%93Weierstrass_theorem))

故 $\overline{Range(A)}=L^2([0,1])$.

接下来我们求解 $A$ 的各个特征值。

设 $\lambda\neq 0,Au=\lambda u$，则 $u=\dfrac{1}{\lambda}A\Rightarrow u=A(\dfrac{1}{\lambda}u) \Rightarrow -u^{\prime\prime}=\dfrac{u}{\lambda}$，这是最基本的常微分方程，他的解是三角级数 $u=A\sin \dfrac{1}{\sqrt\lambda}x+B\cos\dfrac{1}{\sqrt \lambda}x$。

因为 $u(0)=0$，所以 $B=0$，因为 $u(1)=0$，所以我们要求 $\dfrac{1}{\sqrt\lambda}\in \mathbb N\pi$，故 $u(x)=A\sin k\pi x$，为了满足 $||u||_2=1$，我们可以解得 $A=\sqrt 2$.

接下来我们证明 $A^{1/2}$ 存在，且是紧且对称的。

**$\color{red}引理4$：** 对于 $f\in L^2([0,1])$ 且有傅里叶级数表示

$$
\left\{\begin{matrix}
f(x)=\sum_{k=1}^\infty c_k\sqrt 2 \sin k\pi x  & \\
c_k=\int_0^1 f(x)\sqrt 2\sin k\pi x\mathrm dx  &
\end{matrix}\right.
$$

定义算子 $B$ 为

$$Bf(x)=\sum_{k=1}^\infty \frac{1}{k\pi }c_k\sqrt 2\sin k\pi x$$

则 $B$ 在 $L^2([0,1])$ 上为紧且对称的有界算子，且 $B^2=A$.

**证明：** $B^2=A$ 不难验证，剩下的咕咕咕

接下来我们对于实值函数 $V\in C([0,1])$ 定义 $m_Vf=Vf$，则 $m_V\in\mathcal B(L^2([0,1]))$ 且是对称的（$V$ 是连续有界的故 $m_V$ 有界，$V$ 是实值函数故 $m_V$ 是对称的）

**$\color{red}引理5$：** $T=Bm_V B$ 满足
1）$T$ 是紧且对称的 2) $T\in\mathcal B(L^2([0,1]),C([0,1]))$

**证明：**

因为 $B$ 和 $m_V$ 都是紧且对称的，所以 1) 可以直接得出。

对于 2)，我们只需要证明 $B\in\mathcal B(L^2([0,1]),C([0,1]))$.

延续此前对 $f$ 的傅里叶级数表示的记号，

$$Bf=\sum_{k=1}^\infty \frac{c_k}{k\pi}\sqrt 2\sin k\pi x,$$
$$\frac{c_k}{k\pi}\sqrt 2 \sin k\pi x| \leq \frac{|c_k|\sqrt 2}{k\pi}\leq \frac{|c_k|}{k},$$
$$\sum_{k=1}^\infty \frac{|c_k|}{k}\leq (\sum_j \frac{1}{k^2})^{1/2}(\sum_{k}|c_k|^2)^{1/2}=\frac{\pi}{\sqrt 6}||f||_2$$

由 [Weierstrass M-test](https://en.wikipedia.org/wiki/Weierstrass_M-test)，$|Bf(x)|\leq \dfrac{\pi}{\sqrt 6} ||f||_2$，即证明 $B$ 是有界的。

**$\color{red}引理6$：** $I+Bm_VB$ 可逆

根据 [Fredholm Alternative](https://en.wikipedia.org/wiki/Fredholm_alternative)，一个紧对称算子的逆算子存在当且仅当他的零空间是平凡的。

假设 $(I+Bm_VB)g=0$，则

$$
\begin{aligned}
0 &=\langle (I+Bm_VB)g,g\rangle \\
&= ||g||_2^2+\langle Bm_VBg,g\rangle (\text{ B 是对称的}) \\
&= ||g||_2^2+\langle m_V Bg,Bg\rangle \\
&= ||g||_2^2+\int_0^1 V|Bg|^2\mathrm dx \\
&\geq ||g||_2^2
\end{aligned}
$$

所以 $g=0$，$NULL(I+Bm_VB)=\{0\}$，$I+Bm_VB$ 可逆。

**$\color{red}定理7：$** 对于 $V\in C([0,1])$ 且 $V\geq 0$ 的实值函数和 $f\in C([0,1])$，存在唯一 $u\in C^2([0,1])$ 为常微分方程

$$
(DP)
\left\{\begin{matrix}
-u^{\prime\prime}(x)+V(x)u(x)=f(x)  & x\in [0,1]\\
u(0)=u(1)=0  &
\end{matrix}\right.
$$

的解。

**证明：**

取 $v=(I+A^{1/2}m_VA^{1/2})^{-1}A^{1/2}f,u=A^{1/2}v$，则

$$
\begin{aligned}
u+A(Vu) &=A^{1/2} v+A^{1/2}[A^{1/2}m_VA^{1/2}]v \\
&= A^{1/2}(I+A^{1/2}m_V A^{1/2})v \\
&= Af
\end{aligned}
$$

两边同时求二阶导，得到

$$u^{\prime\prime}-Vu=-f$$

整理即得

$$-u^{\prime\prime}+Vu=f$$

不难验证 $u$ 也满足边界条件，故存在唯一的

$$u=A^{1/2}(I+A^{1/2}m_VA^{1/2})^{-1}A^{1/2}f$$

解决 Dirichlet 问题。