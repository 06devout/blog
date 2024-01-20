---
title: Maths is Hard I
date: 2023-11-06 18:45:22
categories:
- Maths Is Hard Series
tag:
- 初等数学
mathjax: true
---

## Description

对于 $A,B\in \mathbb F_2^n$，定义 $A\cdot B=\sum_{i=1}^n a_ib_i$，并定义 $T_n=\{A\in\mathbb F_2^n|A\cdot A=3\}$

证明：对于互不相同的 $A_1,A_2,\cdots,A_{n+1}\in T_n$, $\exists 1\leq i<j\leq n+1$ 使得 $A_i\cdots A_j=1$.

## Solution

用 $A_k(i)$ 表示 $A_k$ 的 $x_i$ 的值。

设 $B_k=\{i=1,2,\cdots,n|A_k(i)=1\}$，即 $A_k$ 中每个元素的值为 1 的下标位置。

由抽屉原理，$n+1$ 个 $A_k$ 代表 $n+1$ 个颜色的小球，每个颜色有三个小球，放入 $A_k(i)=1$ 的三个位置（抽屉）中，则存在一个抽屉中有至少两个不同颜色的小球，即 $\exists 1\leq i<j\leq n+1$ 使得 $A_i\cdot A_j>0$。

因为 $A_i\cdot A_j\in \{0,1,2\}$，

- 若 $A_i\cdot A_j=1$，则命题成立.
- 否则 $\forall A_i\cdot A_j\neq 0,A_i\cdot A_j=2$.

假设 $\forall A_i\cdot A_j\neq 0,A_i\cdot A_j=2(*)$。

**引理1：** 对于互不相同的 $i,j,k$，若 $A_i\cdot A_j=A_j\cdot A_k=2$，则 $A_i\cdot A_k=2$。

**证明：** 不妨设 $A_j(1)=A_j(2)=A_j(3)=1,A_i(1)=A_i(2)=1$，因为 $A_j\cdot A_k=2$，所以 $A_k(1),A_k(2)$ 中至少有一个为 $1$，故 $A_i\cdot A_k\neq 0,A_i\cdot A_k=2$. $\Box$

即我们可以把 $A_i$ 分成若干组 $E_1,E_2,\cdots,E_m$，每一组内的任意两个元素的点乘恰好为 2，而不同组的元素的点乘为 0.

形式化的：设 $C_k=\{j=1,2,\cdots,n+1|A_j\cdot A_k=2\}$，则 $\forall j\in C_k,C_j=C_k$，而 $\{C_k\}_{k=1}^n$ 中所有不同的元素构成 $\{E_k\}_{k=1}^m$。

设 $D_j=\cup_{i\in E_j}B_i$，即 $E_j$ 中某个元素在该位上为 1 的下标集合（$E_j$ 覆盖的下标位置）

**引理2：** $\forall i\neq j,D_i\cap D_j=\emptyset$，即 $E_i$ 和 $E_j$ 覆盖的下标无交集。

**证明：** 反证法：若 $D_i\cap D_j\neq \emptyset,$ 则存在 $k\in E_i,\ell\in E_j$ 使得 $B_k\cap B_\ell\neq \emptyset$，即 $A_k\cdot A_\ell \neq 0$，则 $A_k\cdot A_\ell=2$，与 $k,\ell$ 在不同的 $E_i,E_j$ 中矛盾。 $\Box$

**引理3：** $|D_k|\geq |E_k|$，即大小为 $\sigma$ 的一个集合 $E_k$ 至少覆盖了 $\sigma$ 个位置。

**证明：** 

对于 $\sigma\leq 2$，不难证明。

设 $E_k=\{e_1,e_2,\cdots,e_\sigma\}$,

不妨设 $B_{e_1}=\{1,2,3\}$，即 $A_{e_1}=1,1,1,0,\cdots$。

因为 $A_{e_2}\cdot A_{e_1}=2$，不妨设 $B_{e_2}=\{1,2,4\}$。

则对于 $\sigma=3,4$，$\{1,2,3,4\}\subseteq D_k$，$|D_k|\geq \sigma$。

对于 $\sigma\geq 5$，

若 $B_{e_3}\cap B_{e_1}\neq \{1,2\}$，则不妨设 $B_{e_3}=\{1,3,4\}$。

$B_{e_4}$ 只能等于 $\{2,3,4\}$。（类似第二问证明）

此时不存在合法的 $B_{e_5}$。

故 $B_{e_1}\cap B_{e_3}= \{1,2\}$，不妨设 $B_{e_3}=\{1,2,4\}$。

则 $B_{e_4}\cap B_{e_1}=\{1,2\}$，否则无法同时满足 $A_{e_2}\cdot A_{e_4}=A_{e_3}\cdot A_{e_4}=2$，则不妨设 $B_{e_4}=\{1,2,5\}$。

以此类推，$B_{e_k}$ 唯一确定，不难发现此时 $|D_k|=\sigma+1$，引理3即证。 $\Box$

应用引理3，对于所有的 $E_k$ 求和，得到

$$n=\sum_{k=1}^m |D_k|\geq \sum_{k=1}^m |E_k|=n+1$$

的矛盾，即假设 $(*)$ 不成立，原命题成立。