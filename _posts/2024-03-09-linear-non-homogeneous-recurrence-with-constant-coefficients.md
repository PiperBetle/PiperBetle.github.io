---
layout: post
title: "常系数线性非齐次递推"
tags: 笔记 数学
---

$$
a_n=(\sum_{i=1}^{k_0}c_ia_{n-i})+\sum_{i=1}F_i(n)\\
F_i(n)=(\sum_{j=0}^{k_i}d_{i,j}n^j)s_i^n\\
$$

设特征方程

$$
x^{k_0}=\sum_{i=1}^{k_0}c_ix^{k_0-i}
$$

的 $n$ 个根去重后数量为 $t$，第 $i$ 个根为 $r_i$，$r_i$ 的重根数量为 $m_i$。  

$$
\phi_0=\sum_{i=1}^t((\sum_{j=0}^{m_i-1}\alpha_{i,j}n^j)r_i^n)\\
\phi_i=n^{\sum\limits_{j=1}^tm_j[r_j=s_i]}(\sum_{j=0}^{k_i}p_{i,j}n^j)s^n
$$

那么 $a_n=\phi_0+\sum\limits_{i=1}\phi_i$，其中 $\alpha_{i,j},p_{i,j}$ 均为常数，可以求解线性方程组获得。

为了简化描述，下文中单道题如果只出现 $\alpha_{1,0},\alpha_{1,1},\alpha_{1,2},\cdots$ 或 $\alpha_{1,0},\alpha_{2,0},\alpha_{3,0},\cdots$ 或 $p_{1,0},p_{1,1},p_{1,2},\cdots$ 或 $p_{1,0},p_{2,0},p_{3,0},\cdots$，简记为 $\alpha_1,\alpha_2,\alpha_3\cdots$ 或 $p_1,p_2,p_3\cdots$。

---

$$
a_1=a_2=1\\
a_n=4a_{n-1}-4a_{n-2}+3^n-5
$$

得到特征方程 $x^2=4x-4$，解得 $x_1=x_2=2$。  
所以可以得到齐次递推的解 $2^n(\alpha_1n+\alpha_0)$。  
因为 $F(x)=3^n-5$，所以 $F(x)$ 的解为 $p_13^n+p_2$。  
所以通项为 $2^n(\alpha_1n+\alpha_0)+p_13^n+p_2$。

$$
\begin{cases}
(\alpha_1+\alpha_0)2^1+p_13^1+p_2=a_1=1\\
(2\alpha_1+\alpha_0)2^2+p_13^2+p_2=a_2=1\\
(3\alpha_1+\alpha_0)2^3+p_13^3+p_2=a_3=22\\
(4\alpha_1+\alpha_0)2^4+p_13^4+p_2=a_4=160\\
\end{cases}
\\
\begin{cases}
\alpha_1=-\frac{33}4\\
\alpha_2=-\frac94\\
p_1=9\\
p_2=-5\\ 
\end{cases}
$$

最后解得通项为 $2^n(-\frac{33}4n-\frac94)+9\times3^n-5$。

---

$$
a_1=a_2=1\\
a_n=3a_{n-1}+4a_{n-2}+2n
$$

得到特征方程 $x^2=3x+4$，解得 $x_1=-1,x_2=4$。  
所以可以得到齐次递推的解 $(-1)^n\alpha_1+4^n\alpha_2$。  
因为 $F(x)=2n$，所以 $F(x)$ 的解为 $p_1n+p_0$。  
所以通项为 $(-1)^n\alpha_1+4^n\alpha_2+p_1n+p_0$。

$$
\begin{cases}
(-1)^1\alpha_1+4^1\alpha_2+p_1+p_0=a_1=1\\
(-1)^2\alpha_1+4^2\alpha_2+2p_1+p_0=a_2=1\\
(-1)^3\alpha_1+4^3\alpha_2+3p_1+p_0=a_3=1\\
(-1)^4\alpha_1+4^4\alpha_2+4p_1+p_0=a_4=-1\\
\end{cases}
\\
\begin{cases}
\alpha_1=-\frac1{10}\\
\alpha_2=-\frac1{90}\\
p_1=\frac13\\
p_0=\frac{11}{18}\\
\end{cases}
$$

最后解得通项 $a_n=-\frac1{10}(-1)^n-\frac1{90}4^n+\frac13n+\frac{11}{18}$。

---

$$
a_n=4a_{n-1}-3a_{n-2}+2^n+n+3
$$

得到特征方程 $x^2=4x-3$，解得 $x_1=1,x_2=3$。  
所以可以得到齐次递推的解 $\alpha_1+3^n\alpha_2$。  
因为 $F(x)=2^n+n+3$，所以 $F(x)$ 的解为 $p_{1,0}2^n+p_{2,1}n+p_{2,2}$。  
所以通项为 $\alpha_1+3^n\alpha_2+p_{1,0}2^n+p_{2,1}n+p_{2,0}$。  
计算的时候记得把 $\alpha_1$ 和 $p_{2,0}$ 当成同一个系数去计算。

---

求特征根为 $2,2,2,5,5,9$，$F(x)=(n^2+2n+3)2^n-n3^n+n^3$ 的通项。  
齐次递推的解 $(\alpha_{1,2}n^2+\alpha_{1,1}n+\alpha_{1,0})2^n+(\alpha_{2,1}n+\alpha_{2,0})5^n+\alpha_{3,0}9^n$。  
由于特征根 $2$ 重数为 $3$，所以 $\phi_1=n^3(p_{1,2}n^2+p_{1,1}n+p_{1,0})2^n$。  
$\phi_2=(p_{2,1}n+p_{2,0})3^n$。  
$\phi_3=p_{3,2}n^2+p_{3,1}n+p_{3,0}$。  
所以通项为 $(\alpha_{1,2}n^2+\alpha_{1,1}n+\alpha_{1,0})2^n+(\alpha_{2,1}n+\alpha_{2,0})5^n+\alpha_{3,0}9^n+n^3(p_{1,2}n^2+p_{1,1}n+p_{1,0})2^n+(p_{2,1}n+p_{2,0})3^n+p_{3,2}n^2+p_{3,1}n+p_{3,0}$。