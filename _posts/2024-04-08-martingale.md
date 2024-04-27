---
layout: post
title: "鞅"
tags: 笔记 数学
---

### 鞅
称随机变量序列 $Z_0,Z_1,\cdots$ 是关于 $X_0,X_1,\cdots$ 的鞅，如果对于所有 $n\ge0$，下列条件成立。
- $Z_n$ 是 $X_0,X_1,\cdots,X_n$ 的函数
- $\mathbb E[\vert Z_n\vert]<\infty$
- $\mathbb E[Z_{n+1}\vert X_0,X_1,\cdots,X_n]=Z_n$

实际上 $X$ 的下标不必从 $0$ 开始，大多数情况从 $1$ 开始更方便。当我们说 $Z_0,Z_1,\cdots$ 是关于 $X_1,X_2,\cdots$ 的鞅时，可以认为 $X_0$ 是常数，被省略了。  
根据鞅的定义可以很简单导出一个引理：$\mathbb E[Z_n]=\mathbb E[Z_0]$。不过这个引理并不能反推出 $Z$ 是鞅。

如果随机变量序列随机变量序列 $Z_0,Z_1,\cdots$ 是关于其本身的鞅，那么称 $Z_0,Z_1,\cdots$ 是鞅。

- $\mathbb E[\vert Z_n\vert]<\infty$
- $\mathbb E[Z_{n+1}\vert Z_0,Z_1,\cdots,Z_n]=Z_n$


比如说一个公平赌博，$X_i$ 表示第 $i$ 次赌博赢得的钱数（若输，$X_i<0$），$Z_i$ 表示第 $i$ 次赌博后累计赢的钱数。  

$$
\mathbb E[Z_{i+1}\vert X_1,X_2,\cdots,X_i]=\mathbb E[Z_i\vert X_1,X_2,\cdots,X_i]+\mathbb E[X_{i+1}]=Z_i+\mathbb E[X_{i+1}]=Z_i
$$

这样就证明序列 $Z$ 是 $X$ 的鞅。

### 停时

称非负整随机变量 $T$ 是序列 $Z$ 的停时，如果 $Z_{n+1},Z_{n+2},\cdots$ 与 $Z_1,Z_2,\cdots,Z_n$ 无关。  

鞅停时定理：如果 $Z_0,Z_1,\cdots$ 是关于 $X_1,X_2,\cdots$ 的鞅，$T$ 是 $X_1,X_2,\cdots$ 的停时，如果满足下列三个条件的**其中一个**：

- $\vert Z_i\vert$ 有界
- $T$ 有界
- $\mathbb E[T]<\infty$，并且存在常数 $c$ 使得 $\mathbb E[\vert Z_{i+1}-Z_i\vert\space\vert X_1,X_2,\cdots X_i]<c$

那么 $\mathbb E[Z_T]=\mathbb E[Z_0]$。

利用鞅停时定理可以获得赌徒破产问题简单的解。  
赌徒破产问题：一个赌徒初始时有 $0$ 元，每次赌博有 $p$ 概率 $+1$ 元，$1-p$ 概率 $-1$ 元。累计输 $l_1$ 元或赢 $l_2$ 元结束。求在输 $l_1$ 前赢 $l_2$ 元的概率，以及结束时赌博的期望次数。

若 $p=\frac12$，那么这是公平赌博。不妨设 $X_i$ 表示第 $i$ 次赌博赢得的钱数（若输，$X_i<0$），$Z_i$ 表示第 $i$ 次赌博后累计赢的钱数，$T$ 为首次累计输 $l_1$ 元或赢 $l_2$ 元的停时。  
由于 $Z$ 是鞅且 $\vert Z_i\vert$ 有界，所以 $\mathbb E[Z_T]=\mathbb E[Z_0]=0$，不妨设 $r$ 为输 $l_1$ 前赢 $l_2$ 元的概率，那么得到方程 

$$
rl_2-(1-r)l_1=0\\
r=\frac{l_1}{l_1+l_2}
$$

但是这里 $p\ne\frac12$ 并不是公平赌博。所以我们可以构造一个鞅。  
继续不妨设 $X_i$ 表示第 $i$ 次赌博赢得的钱数（若输，$X_i<0$），$Z_i$ 表示第 $i$ 次赌博后累计赢的钱数，$T$ 为首次累计输 $l_1$ 元或赢 $l_2$ 元的停时。  
设 $A_n=(\frac{1-p}p)^{Z_n}$

$$
\begin{aligned}
\mathbb E[A_{i+1}\vert X_1,X_2,\cdots,X_i]&=\mathbb P(X_{i+1}=-1)\mathbb E[A_{i+1}\vert X_1,X_2,\cdots,X_i,X_{i+1}=-1]\\&+\mathbb P(X_{i+1}=1)\mathbb E[A_{i+1}\vert X_1,X_2,\cdots,X_i,X_{i+1}=1]\\
&=pA_i\frac{1-p}p+(1-p)A_i\frac p{1-p}\\
&=A_i
\end{aligned}
$$

所以 $\mathbb E[A_T]=\mathbb E[A_0]=(\frac{1-p}p)^0=1$  
不妨设 $r$ 为输 $l_1$ 前赢 $l_2$ 元的概率，那么得到方程

$$
r(\frac{1-p}p)^{l_2}+(1-r)(\frac{1-p}p)^{-l_1}=1\\
r=\frac{\left(\frac{1-p}{p}\right)^{l_1}-1}{\left(\frac{1-p}{p}\right)^{l_1+l_2}-1}
$$

设 $B_n=Z_n-(2p-1)n$

$$
\begin{aligned}
\mathbb E[B_{i+1}\vert X_1,X_2,\cdots,X_i]&=\mathbb P(X_{i+1}=-1)\mathbb E[B_{i+1}\vert X_1,X_2,\cdots,X_i,X_{i+1}=-1]\\&+\mathbb P(X_{i+1}=1)\mathbb E[B_{i+1}\vert X_1,X_2,\cdots,X_i,X_{i+1}=1]+(2p-1)\\
&=p(B_i+1)+(1-p)(B_i-1)+(2p-1)\\
&=B_i
\end{aligned}
$$

所以 $\mathbb E[B_T]=\mathbb E[B_0]=0$

由于我们已经求得了 $r$

$$
\mathbb E[Z_T]=rl_2-(1-r)l_1\\
\mathbb E[B_T]=\mathbb E[Z_T-(2p-1)T]=\mathbb E[Z_T]-(2p-1)\mathbb E[T]\\
\mathbb E[T]=\frac{l_2 \left(\frac{1-p}{p}\right)^{l_1}-l_1 \left(\frac{1-p}{p}\right)^{l_1+l_2}+l_1 \left(\frac{1-p}{p}\right)^{l_1}-l_2}{(2 p-1) \left(\left(\frac{1-p}{p}\right)^{l_1+l_2}-1\right)}
$$

```mma
Solve[r ((1 - p)/p)^(l2) + (1 - r) ((1 - p)/p)^(-l1) == 1, r]
ezt = r*l2 - (1 - r) l1
Solve[ezt - (2 p - 1) et == 0, et]
```

### 瓦尔德等式

$X_1,X_2,\cdots X_n$ 是独立，与 $X$ 同分布的随机变量，$T$ 是这个序列的停时。如果 $\mathbb E[X],\mathbb E[T]\le\infty$，那么

$$
\mathbb E\Big[\sum_{i=1}^T X_i\Big]=\mathbb E[T]\mathbb E[X]
$$

虽然这个等式有多种方法证明，但是鞅的证明方法是容易理解的。  
$Z_n=\sum\limits_{i=1}^n(X_i-\mathbb E[X])$，不难证明 $Z$ 是关于 $X$ 鞅，所以 $\mathbb E[Z_i]=0$。

$$
\begin{aligned}
\mathbb E[Z_T]&=\mathbb E\Big[\sum_{i=1}^T(X_i-X)\Big]\\
&=\mathbb E\Big[\sum_{i=1}^T X_i-T\mathbb E[X]\Big]\\
&=\mathbb E\Big[\sum_{i=1}^T X_i\Big]-\mathbb E[T]\mathbb E[X]\\
&=0
\end{aligned}
$$

### 吾妻不等式

{% raw %}

$X_0,X_1,\cdots,X_n$ 是一个鞅，如果对于所有 $i\ge1$ 满足

$$
B_i\le X_i-X_{i-1}\le B_i+d_k
$$

那么对于所有 $t\ge0$ 满足

$$
\mathbb P(\vert X_t-X_0\vert\ge\lambda)\le2\exp\left(\frac{-2\lambda^2}{{\sum_{i=1}^t}d_i^2}\right)
$$

如果取 $B_i=-c_i,d_i=2c_i$ 可以导出一个更常用的结构：

$X_0,X_1,\cdots,X_n$ 是一个鞅，如果对于所有 $i\ge1$ 满足

$$
\vert X_i-X_{i-1}\vert\le c_i
$$

那么对于所有 $t\ge0$ 满足

$$
\mathbb P(\vert X_t-X_0\vert\ge\lambda)\le2\exp\left(\frac{-\lambda^2}{{2\sum_{i=1}^t}c_i^2}\right)\\
$$

如果所有的 $c$ 都一样

$$
\mathbb P(\vert X_t-X_0\vert\ge\lambda)\le2\exp\left(\frac{-\lambda^2}{2tc^2}\right)\\
$$

或者可以写成

$$
\mathbb P(\vert X_t-X_0\vert\ge\lambda\sqrt t)\le2\exp\left(\frac{-\lambda^2}{2c^2}\right)\\
$$

### 杜布鞅

杜布鞅是用如下方法构造的鞅：$X_0,X_1,\cdots,X_n$ 是随机变量序列，$Y$ 是随机变量且 $\mathbb E[Y]<\infty$，$Z_i=\mathbb E[Y\vert X_0,X_1,\cdots,X_i]$。  
证明 $Z_i$ 是鞅：

$$
\begin{aligned}
E[Z_{i+1}\vert X_0,X_1,\cdots,X_i]&=\mathbb E[\mathbb E[Y\vert X_0,X_1,\cdots,X_{i+1}]\vert X_0,X_1,\cdots,X_i]\\
&=\mathbb E[Y\vert X_0,X_1,\cdots,X_i]=Z_i
\end{aligned}
$$

在大多数应用中，为了方便计算一般取 $Z_0=\mathbb E[Y]$。  
形象来看，我们把 $Y$ 当成是 $X_0,X_1,\cdots,X_n$ 的函数，起初我们对 $Y$ 一无所知，在获取 $X_i$ 时，我们也就获得了更多关于 $Y$ 的信息，$Z_i$ 就是利用了 $X_0,X_1,\cdots,X_i$ 的信息后，$Y$ 的期望。  

比如说随机图 $G_{n,p}$，以某个顺序排出其 $\binom n2$ 条边。令 $X_i=1$ 表示位置 $i$ 上存在边（这个概率为 $p$），那么关于 $X$ 的函数就是鞅。比如说其最大独立集大小 $\alpha(G)$，其着色数最小值 $\chi(G)$ 均是鞅。这种每次揭示一条边的鞅成为边暴露鞅。  
类似的，每次揭示一个顶点相邻的点的集合，这种方式构造的鞅是顶点暴露鞅。换句话说，以某个顺序排出其 $n$ 个点，$X_i$ 是排列中前 $i$ 个点的导出子图，关于 $X_i$ 的函数是顶点暴露鞅。

运用杜布鞅可以快速算出随机图着色数偏离期望的一个界。  
随机图 $G_{n,p}$ 的着色数最小值 $\chi(G)$ 是点暴露鞅。记 $G_i$ 表示前 $i$ 个点的随机子图，$Z_i=\mathbb E[\chi(G)\vert G_1,G_2\cdots,G_i]$。考虑每次加点的过程中，一个顶点最多染一个颜色，所以 $\vert Z_i-Z_{i-1}\vert\le1$，运用吾妻不等式可以得到：

$$
\mathbb P(\vert \chi(G)-\mathbb E[\chi(G)]\vert\ge\lambda\sqrt n)\le2\mathrm e^{-2\lambda}
$$

{% endraw %}