---
layout: post
title: "环形染色问题"
tags: 笔记 数学
---

一个大小为 $n$ 的圆环（环上的点有编号）需要用 $m$ 种颜色进行染色（每种颜色不必全都使用），要求相邻两个点的的颜色不同，有多少种染色方案？

为了不考虑边界问题，假定 $n,m\ge2$。  
如果不考虑这是一个环，当成一条链，那么第 $1$ 个点颜色任意，其他所有点都只需要满足和前面那个点颜色相同，所以方案数是 $m(m-1)^{n-1}$。  
如果第 $1$ 个点和第 $n$ 个点颜色相同，那么就把这两个点当成同一个点，方案数是 $a_{n-1}$。  
所以得到递推式：

$$
\begin{aligned}
a_n&=m(m-1)^{n-1}-a_{n-1}\\
a_n&=(m-1)(m-1)^{n-1}+(m-1)^{n-1}-a_{n-1}\\
a_n&=(m-1)^n+(m-1)^{n-1}-a_{n-1}\\
a_n-(m-1)^n&=(m-1)^{n-1}-a_{n-1}\\
\end{aligned}
$$

不妨设 $b_n=a_n-(m-1)^n$，那么 $\lbrace b_n\rbrace$ 是公比为 $-1$ 的等比数列。  
当 $n=2$ 时，$a_2=m(m-1)$，$b_2=a_2-(m-1)^2=m-1$。  
根据公比得到 $b_n=b_2\times(-1)^{n-2}=(-1)^n(m-1)$。  
把 $\{b_n\}$ 带入，得到 $a_n=b_n+(m-1)^n=(m-1)^n+(-1)^n(m-1)$。

如果要求每个颜色都要使用只要一次，答案就是 $a_m-a_{m-1}$。  
如果圆心有颜色，直接钦定圆心颜色为 $m$ 种中的一个，用外圈的 $n$ 个点，剩余 $m-1$ 种颜色进行乘法原理。