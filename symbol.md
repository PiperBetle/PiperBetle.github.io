---
layout: page
title: Symbol
permalink: /symbol/
---

提示：可以右键 $\LaTeX$ 查看源码。

|符号|解释|说明|
|:-:|:-:|:-|
|$\lfloor x\rfloor$|向下取整|不是四舍五入，也不是向零取整|
|$\lceil x\rceil$|向上取整|不是四舍五入，也不是向零取整|
|$[x]$|艾佛森括号|若命题 $x$ 为假，或表达式 $x=0$，则其值为 $1$，否则为 $0$。注意，本博客完全不会把中括号当成小括号上一级的括号|
|$[n]$|$\lbrace1,2,\cdots,n\rbrace$|是一个集合|
|$[x^n]F(x)$|取系数|值为 $F(x)$ 展开式中 $x^n$ 那项的系数|
|$\binom nm$|组合数|$n$ 个不同的球数选 $m$ 个的方案数，$\binom nm=\binom{n-1}m+\binom{n-1}{m-1}$|
|$n\brack m$|第一类斯特林数|$n$ 个不同的人坐 $m$ 张圆桌的方案数，${n\brack m}=(n-1){n-1\brack m}+{n-1\brack m-1}$|
|$n\brace m$|第二类斯特林数|$n$ 个不同的球放入 $m$ 个相同盒子的方案数，且不能有空盒，${n\brace m}=m{n-1\brace m}+{n-1\brace m-1}$|
|$\mathcal O$|渐进意义复杂度|忽略低阶复杂度后的渐进意义复杂度|
|$\mathbb P(X)$|事件 $X$ 发生的概率|$0\le\mathbb P(X)\le1$|
|$\mathbb E[X]$|随机变量（或表达式）$X$ 的期望|其实就是加权平均，不管是离散的还是连续的还是既不离散又不连续的|
|$Var[X]$|随机变量（或表达式）$X$ 的方差|$Var[X]=\mathbb E[X^2]-\mathbb E^2[X]$|
|$\operatorname{pop(x)}$|population count|$x$ 二进制下位 $1$ 的数量，有可能会写成 $\operatorname{popcnt}$ 或 $\operatorname{popcount}$