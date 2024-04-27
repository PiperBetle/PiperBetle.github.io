---
layout: post
title: "概率方法"
tags: 笔记 数学
---

### 期望求得上下界
$f(x)$ 是定义在 $A$ 上的函数。  
若随机变量 $X\in A$，显然 $\min\limits_{x\in A}f(x)\le\mathbb E[f(X)]\le\max\limits_{x\in A}f(x)$。  
如果 $X$ 不为常数，那么 $\min\limits_{x\in A}f(x)<\mathbb E[f(X)]<\max\limits_{x\in A}f(x)$。  
这样就通过计算期望获得了 $f(x)$ 的一个上界和下界。

当且仅当集合 $S$ 满足 $\forall a,b\in S,a+b\not\in S$ 时，称作 $S$ 是 sum-free 的。  
求证，对于任意一个整数集合 $S$，存在一个 $S$ 的子集为 sum-free 且其大小超过 $\frac{\vert S\vert}3$。  

选取质数 $p$ 满足 $p=3k+2\ge\max\limits_{x\in S}x$，根据狄利克雷定理，这样的 $p$ 一定存在。而且由于 $a+b=c\pmod p$ 是 $a+b=c$ 的必要条件，所以后续都在模 $p$ 意义下考虑，相当于加强了命题。  
随机选取一个 $x\in[1,p-1]\cap\mathbb N^+$，若 $t\in s,tx\in[k+1,2k+1]$，那么就把 $x$ 放入集合 $T$ 中。显然 $T$ 是 sum-free 的。  
根据逆元，$tx\in[1,p-1]$ 并且互不相同。$t\in T$ 的概率是 $\frac{k+1}{3k+1}$，所以 $\mathbb E[\vert T\vert]=\frac{k+1}{3k+1}\vert S\vert\ge\frac13\vert S\vert$。
<p align="right" style="font-size:1.5rem;">■</p>

常用的方法是产生一个符合答案的随机构造方式，计算其期望贡献。

证明对于简单无向图 $G_{V,E}$，其存在一个边数超过 $\frac{\vert E\vert}2$ 的子图 $G'_{V,E'}$ 使得其为二分图。

将 $V$ 中的节点等概率随机分到 $A$ 和 $B$ 中。即 $\forall v\in V,\mathbb P(v\in A)=\mathbb P(v\in B)=\frac12$。  
显然，$\forall e\in E$，有 $\frac12$ 的概率使得 $e$ 连接了 $A$ 和 $B$ 中的某个节点。  
根据期望可加性得到总期望为 $\frac{\vert E\vert}2$，也就是说必然存在一个 $A,B$ 的划分方法使得子图 $G'_{V,E'}$ 为二分图。
<p align="right" style="font-size:1.5rem;">■</p>

证明对于简单无向图 $G_{V,E}$，其存在一个点数超过 $\sum\limits_{v\in V}\frac1{\deg(v)+1}$ 的独立集。

考虑随机生成一个排列 $\pi$，按照 $\pi$ 的顺序把 $\vert V\vert$ 个点依次加入一个点集。但是如果加入点 $v$ 时点集已经有点 $v$ 相邻的点，就不加入点 $v$。  
那么当且仅当点 $v$ 在 $\pi$ 中出现的位置早于其所有相邻的点时，$v$ 才会被加入点集。这个事件发生的概率为 $\frac1{\deg(v)}$。  
根据期望可加性得到总期望为 $\sum\limits_{v\in V}\frac1{\deg(v)+1}$，也就是说必然存在一个排列使得独立集点数超过 $\sum\limits_{v\in V}\frac1{\deg(v)+1}$。
<p align="right" style="font-size:1.5rem;">■</p>

使用这种方法的优势是不需要显式构造解，只需要计算出概率就能完成证明。利用不需要显示构造的优点可以快速证明一些难以解释的问题。
$52$ 棵树在一个圆周上，生活着 $15$ 只松鼠。求证必然存在连续的 $7$ 棵树，其上生活着至少 $3$ 只松鼠。

假设已经钦定松鼠的排布方式 $\pi$，那么不妨随机选取 $1$ 棵树以及其旁边的各 $3$ 棵树，用随机变量 $X$ 表示上面的松鼠数量。  
每棵数上松鼠数量期望是 $\frac{15}{52}$，所以 $\mathbb E[X]=7\times\frac{15}{52}=\frac{105}{52}>2$。  
这样我们得到了任意排布方式 $\pi$下最多的连续 $7$ 棵树上的松鼠数量下界为 $\frac{105}{52}$，由于松鼠数量肯定是整数，所以下界为 $3$。  
<p align="right" style="font-size:1.5rem;">■</p>

最后以一道 2015 年的高联作为结尾：  
已知 $n\ge2$，$a_i\in\mathbb R$，求证存在一组 $\varepsilon_i\in\lbrace-1,1\rbrace$ 使得：

$$
(\sum_{i=1}^na_i)^2+(\sum_{i=1}^n\varepsilon_ia_i)^2\le(n+1)\sum_{i=1}^na_i^2
$$

首先考虑证明：

$$
\begin{aligned}
(\sum_{i=1}^na_i)^2&\le n\sum_{i=1}^na_i^2\\
\sum_{i=1}^na_i^2+\sum_i\sum_{i<j}2a_ia_j&\le n\sum_{i=1}^na_i^2\\
-(n-1)\sum_{i=1}^na_i^2+\sum_i\sum_{i<j}2a_ia_j&\le 0\\
-\sum_i\sum_{i<j}(a_i-a_j)^2&\le0
\end{aligned}
$$

倒着写就是证明，这样只需要证明 $(\sum\limits_{i=1}^n\varepsilon_ia_i)^2\le\sum\limits_{i=1}^na_i^2$，不妨尝试证明 $\mathbb E[(\sum\limits_{i=1}^n\varepsilon_ia_i)^2]\le\sum\limits_{i=1}^na_i^2$。  

不妨假设 $\varepsilon_i\in\lbrace-1,1\rbrace$ 的等概率随机变量。

$$
\begin{aligned}
\mathbb E[(\sum\limits_{i=1}^n\varepsilon_ia_i)^2]&=\mathbb E[\sum\limits_{i=1}^n\varepsilon_i^2a_i^2+\sum_i\sum_{i<j}2\varepsilon_i\varepsilon_ja_ia_j]\\
&=\mathbb E[\sum\limits_{i=1}^n\varepsilon_i^2a_i^2+\sum_i\sum_{i<j}2\varepsilon_i\varepsilon_ja_ia_j]\\
&=\mathbb E[\sum\limits_{i=1}^n\varepsilon_i^2a_i^2]+\mathbb E[\sum_i\sum_{i<j}2\varepsilon_i\varepsilon_ja_ia_j]\\
&=\mathbb E[\sum\limits_{i=1}^na_i^2]
\end{aligned}
$$

两式相加，原命题得证。
<p align="right" style="font-size:1.5rem;">■</p>

### 概率次可加性

如果

$$
\binom nk2^{1-\binom k2}<1
$$

那么 $R(k,k)>n$。

随机对 $K_n$ 进行染色。设 $S$ 为 $[n]$ 的 $k$ 元子集。$A_S$ 表示 $S$ 是单色，$I_S$ 是 $A_S$ 的示性变量，那么 $\mathbb E[I_S]=2^{1-\binom nk}$，因为有两种颜色所以要乘 $2$。  
由于 $k$ 元集有 $\binom nk$ 个，运用概率的次可加性可以得到

$$
\mathbb P\left[\bigvee I_S\right]\le\sum\mathbb P(I_S)=\binom nk2^{1-\binom nk}<1
$$

最后一个 $<1$ 是根据题设得到的。  
由于 $\mathbb P\left[\bigvee A_S\right]<1$，所有事件发生的概率小于 $1$，即能做到所有事件均不发生，即 $\mathbb P\left[\bigwedge\overline{A_S}\right]>0$，也就是说存在染色方案使得所有 $k$ 元集均为单色。所以 $R(k,k)>n$。
<p align="right" style="font-size:1.5rem;">■</p>

$G_{V,E}$ 为 $n$ 个点的竞赛图，$V=[n]$。排列 $\pi$ 是 $[n]$ 的一个排列。$\operatorname{fit}(G,\pi)=\#[顺序对]-\#[逆序对]$。  
其中，若在排列 $\pi$ 中，$i$ 的出现位置在 $j(i\ne j)$ 之前时，若有向边 $(i,j)\in E$ 则称其为顺序对，否则称其为逆序对。  
证明：$\min\limits_{G_{V,E}}\max\limits_\pi\operatorname{fit}(G,\pi)<n^{\frac32}\ln^{\frac12}n$

随机生成一个竞赛图。也就是说，以某个顺序标出 $\binom n2$ 条边的顺序，随机分配每一条边的方向。那么在什么排列 $\pi$ 下，每条边对 $\operatorname{fit}(G)$ 的影响，有 $\frac12$ 的概率贡献为 $+1$，$\frac12$ 的概率贡献为 $-1$。  
如果用 $Z_i$ 来表示已知前 $i$ 条边的分布情况后，$\operatorname{fit}(G)$ 的期望，那么 $Z_i$ 就是一个均值为 $0$，$\vert Z_i-Z_{i-1}\vert=1$ 的杜布鞅，而且还是个边暴露鞅。  
运用吾妻不等式得到：

$$
\mathbb P(\operatorname{fit}(G,\pi)>\lambda\sqrt\binom n2)<\exp(-\frac{\lambda^2}2)
$$

由于排列有 $n!$ 种，所以只需要 $n!\exp(-\frac{\lambda^2}2)<1$，就能使得事件 $\operatorname{fit}(G,\pi)>\lambda\sqrt\binom n2$ 不发生，就可以得到 $\min\limits_{G_{V,E}}\max\limits_\pi\operatorname{fit}(G,\pi)\le\lambda\sqrt\binom n2$，不妨设 $\alpha=\lambda\sqrt\binom n2<\lambda\sqrt{\frac {n^2}2}$，那么 $\lambda^2>\frac{2\alpha^2}{n^2}$。

$$
n!\exp(-\frac{\lambda^2}2)<n!\exp(-\frac{\alpha^2}{n^2})\xlongequal{选取适当 \alpha使这个=成立}n!n^{-n}<n!\frac1{n!}=1
$$

此时 $\alpha=n^{\frac32}\ln^{\frac12}n$。另外不难得到不能取等。
<p align="right" style="font-size:1.5rem;">■</p>

### 调整 
如果

$$
\binom nk2^{1-\binom k2}<1
$$

那么 $R(k,k)>n$，实际上还可以运用调整的手段获得一个更好的界：

$$
R(k,k)>n-\binom nk2^{1-\binom k2}
$$

随机对 $K_n$ 进行染色。设 $S$ 为 $k$ 元集。$I_S$ 表示 $S$ 是单色的示性变量，那么 $\mathbb E[I_S]=2^{1-\binom k2}$，因为有两种颜色所以要乘 $2$。  
这样证明了存在一种染色方法使得其单色集合数量至多为 $\binom nk\mathbb E[I_S]=\binom nk2^{1-\binom k2}$。  
如果运用删除法，在上面所有单色集合中删去一个点，就不存在任何单色 $k$ 元集合了。于是剩下还有 $n-\binom nk2^{1-\binom k2}$。
<p align="right" style="font-size:1.5rem;">■</p>

如果图 $G_{V,E}$ 有 $n$ 个点，$\frac{nk}2$ 条边，则其独立数（即最大独立集大小）$\alpha(G_{V,E})\ge\frac n{2k}$。

令每个点 $x\in V$，随机生成一个集合 $S$，使得 $\mathbb P(x\in S)=p$，令随机变量 $X$ 表示 $\vert S\vert$，那么 $\mathbb E[X]=np$。  
每条边 $e\in E$，令 $I_e$ 表示 $e\in S$ 的示性随机变量，那么 $\mathbb E[I_e]=p^2$。  
令随机变量 $Y$ 表示 $S$ 中的边数，$\mathbb E[Y]=\frac{nk}2p^2$。  
对每条 $S$ 中的边，去掉其中一个点。

$$
\mathbb E[X-Y]=np-\frac{nk}2p^2
$$

当 $p=\frac1k$ 使上式最大，为 $\frac n{2k}$。
<p align="right" style="font-size:1.5rem;">■</p>

先随机生成方案后，把不满足的部分删去，使得剩下的结构满足条件，这就是删除法的运用。

运用删除法，还可以证明，存在具有大围长（最小环的元数）的稠密图。

对于任意 $k\ge3$，存在一个具有 $n$ 个节点，至少 $\frac14n^{\frac1k+1}$  条边，围长至少为 $k$ 的图。

生成一个随机图 $G_{n,p}$，令随机变量 $X$ 为图的边数，那么 $\mathbb E[X]=p\binom n2$。  
令随机变量 $Y$ 表示所有点数为 $[3,k-1]$ 的子图中圈的个数。长度为 $i$ 的子图个数为 $\binom ni$，形成可能圈的个数是 $\binom ni\frac{(n-1)!}2$（正序逆序是同一个圈），其形成圈的概率为 $p^i$，所以

$$
\mathbb E[Y]=\sum_{i=3}^{k-1}\binom ni\frac{(n-1)!}2p^i\le\sum_{i=3}^{k-1}n^ip^i
$$

取 $p=n^{\frac1k-1}$

$$
\mathbb E[X]=p\binom n2=\frac12(1-\frac1n)n^{\frac1k+1}\\
\mathbb E[Y]=\sum_{i=3}^{k-1}n^ip^i=\sum_{i=3}^{k-1}n^{\frac ik}<kn^{\frac{k-1}k}
$$

类似的，对于每个圈删除一条边。

$$
\mathbb E[X-Y]\ge\frac12(1-\frac1n)n^{\frac1k+1}-kn^{\frac{k-1}k}\ge\frac14n^{\frac1k+1}
$$

<p align="right" style="font-size:1.5rem;">■</p>

### 洛瓦兹局部引理

对于坏事件集合 $\lbrace E_1,E_2,\cdots,E_n\rbrace$，其相关图 $G_{V,E}$ 满足 $V=[n]$ 且坏事件 $E_i$ 与坏事件 $\lbrace E_j|(i,j)\not\in E\rbrace$ 独立。相关图的度数为其所有节点度数的最大值。  
洛瓦兹局部引理（的对称形式）：

- $\mathbb P(E_i)\le p$
- 其相关图的度数不超过 $d$
- $4dp\le1$

那么必然能做到所有坏事件不发生，即：

$$
\mathbb P(\bigcap_{i=1}^n\overline{E_i})>0
$$

证明咕咕咕……

---

$k\text{-SAT}$ 问题有若干个子句，每个子句是恰好 $k$ 个布尔变量（或其逆）的 $\cap$。若存在一组布尔变量使得所有子句的值为 $1$ 则称其有解。  
证明：若 $k\text{-SAT}$ 中没有变量出现在多于 $\frac{2^k}{4k}$ 子句，则必然有解。

假设这个 $k\text{-SAT}$ 有 $m$ 个子句 $A_1,A_2,\cdots,A_m$，由于每个子句有 $k$ 个布尔变量，所以如果对布尔变量随机赋值 $0$ 或 $1$，那么 $\mathbb P(A_i=1)=2^{-k}$。  
子句 $A_i$ 与所有不具有共同布尔变量的子句独立。由于每个子句有 $k$ 个布尔变量，每个布尔变量都出现在不多于 $\frac{2^k}{4k}$ 个子句，所以其相关图的度数 $d\le k\times\frac{2^k}{4k}=2^{k-2}$。  
那么 $4dp\le4\times2^{k-2}\times2^{-k}=1$，由洛瓦兹局部引理，所有坏事件 $\overline{A_i=1}$ 即 $A_i=0$ 可能全不发生，即此 $k\text{-SAT}$ 有解。
<p align="right" style="font-size:1.5rem;">■</p>

如果

$$
4\binom k2\binom n{k-2}2^{1-\binom k2}<1
$$

那么 $R(k,k)>n$。

随机对 $K_n$ 进行染色。设 $S$ 为 $[n]$ 的 $k$ 元子集。$A_S$ 表示 $S$ 是单色，那么 $\mathbb P[A_S]=2^{1-\binom nk}$，因为有两种颜色所以要乘 $2$。  
$k$ 元子集 $T_1$ 和 $T_2$，如果 $\vert T_1\cap T_2\vert>2$，那么 $A_{T_1}$ 和 $A_{T_2}$ 不独立，在相关图中有边。

$$
d=\vert\lbrace T:\vert S\cap T\vert\le2\rbrace\vert\le\binom k2\binom n{k-2}\\
4dp=4\binom k2\binom n{k-2}2^{1-\binom nk}<1
$$

由洛瓦兹局部引理，所有坏事件能够均不发生，即能做到不存在单色 $k$ 元子集。
<p align="right" style="font-size:1.5rem;">■</p>