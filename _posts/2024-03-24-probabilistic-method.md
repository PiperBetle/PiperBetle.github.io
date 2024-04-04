---
layout: post
title: "概率方法"
tags: 笔记 数学
---

$52$ 棵树在一个圆周上，生活着 $15$ 只松鼠。求证必然存在连续的 $7$ 棵树，其上生活着至少 $3$ 只松鼠。

不妨随机选取 $1$ 棵树 以及其旁边的各 $3$ 棵树，随机变量 $X$ 表示上面的松鼠数量。  
每只松鼠出现在每颗树上的概率相等，所以 $\mathbb E[X]=15\times\frac7{52}=\frac{105}{52}>2$。  
这样我们得到了任意条件下最多的连续 $7$ 棵树上的松鼠数量下界为 $\frac{105}{52}$，由于松鼠数量肯定是整数，所以下界为 $3$。  
注意：这里是先钦定松鼠的排布方式，再去随机选取 $7$ 棵树的位置。

---

当且仅当集合 $S$ 满足 $\forall a,b\in S,a+b\not\in S$ 时，称作 $S$ 是 sum-free 的。  
求证，对于任意一个整数集合 $S$，存在一个 $S$ 的子集为 sum-free 且其大小超过 $\frac{\vert S\vert}3$。  

选取质数 $p$ 满足 $p=3k+2\ge\max\limits_{x\in S}x$，根据狄利克雷定理，这样的 $p$ 一定存在。而且由于 $a+b=c\pmod p$ 是 $a+b=c$ 的必要条件，所以后续都在模 $p$ 意义下考虑，相当于加强了命题。  
随机选取一个 $x\in[1,p-1]\cap\mathbb N^+$，若 $t\in s,tx\in[k+1,2k+1]$，那么就把 $x$ 放入集合 $T$ 中。显然 $T$ 是 sum-free 的。  
根据逆元，$tx\in[1,p-1]$ 并且互不相同。$t\in T$ 的概率是 $\frac{k+1}{3k+1}$，所以 $\mathbb E[\vert T\vert]=\frac{k+1}{3k+1}\vert S\vert\ge\frac13\vert S\vert$。

---

证明对于简单无向图 $G_{V,E}$，其存在一个边数超过 $\frac{\vert E\vert}2$ 的子图 $G'_{V,E'}$ 使得其为二分图。

将 $V$ 中的节点等概率随机分到 $A$ 和 $B$ 中。即 $\forall v\in V,\mathbb P(v\in A)=\mathbb P(v\in B)=\frac12$。  
显然，$\forall e\in E$，有 $\frac12$ 的概率使得 $e$ 连接了 $A$ 和 $B$ 中的某个节点。  
根据期望可加性得到总期望为 $\frac{\vert E\vert}2$，也就是说必然存在一个 $A,B$ 的划分方法使得子图 $G'_{V,E'}$ 为二分图。

---

证明对于简单无向图 $G_{V,E}$，其存在一个点数超过 $\sum\limits_{v\in V}\frac1{\deg(v)+1}$ 的独立集。

考虑随机生成一个排列 $\pi$，按照 $\pi$ 的顺序把 $\vert V\vert$ 个点依次加入。但是如果加入点 $v$ 时已经有点 $v$ 相邻的点，就不加入点 $v$。  
那么当且仅当点 $v$ 在 $\pi$ 中出现的位置早于其所有相邻的点，这个事件发生的概率为 $\frac1{\deg(v)}$。  
根据期望可加性得到总期望为 $\frac1{\deg(v)+1}$，也就是说必然存在一个排列使得独立集点数超过 $\frac1{\deg(v)+1}$。

---

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

---

对于坏事件集合 $\lbrace E_1,E_2,\cdots,E_n\rbrace$，其相关图 $G_{V,E}$ 满足 $V=[n]=\lbrace1,2,\cdots,n\rbrace$ 且坏事件 $E_i$ 与坏事件 $\lbrace E_j|(i,j)\not\in E\rbrace$ 独立。相关图的度数为其所有节点度数的最大值。  
洛瓦兹局部引理（的对称形式）：

- $\mathbb P(E_i)\le p$
- 其相关图的度数不超过 $d$
- $4dp\le1$

那么必然存在一种可能使所有坏事件不发生，即：

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