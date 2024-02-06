---
layout: post
title: "错排"
tags: 笔记 数学
---

# 定义
错排，也就是全错的排列，即长度为 $n$ 的排列满足 $\forall i,a_i\ne i$ 的方案数。  
一般采用 $d_n$ 表示错排。
# 递推
第 $n$ 个元素不能放在下标为 $n$ 的格子里，所以假设放在下标为 $p(p\ne n)$ 的格子。  
第 $p$ 个元素如果放在下标为 $n$ 的格子里，其他元素的方案数就是 $d_{n-2}$。  
第 $p$ 个元素如果不放在下标为 $n$ 的格子里，那么建立一个对应关系。发现 $1\sim n-1$ 这些元素都有且仅有一个位置不能放，这就是一个错排，方案数就是 $d_{n-1}$。  
由于 $p$ 有 $n-1$ 种取值，所以，$d_n=(n-1)(d_{n-1}+d_{n-2})$。
# 通项
采用容斥原理，钦定 $k$ 个元素强行放在原本的位置上。

$$
d_n=\sum_{k=0}^n(-1)^k\binom nk(n-k)!
$$

这个式子也可以用二项式反演获得。

$$
n!=\sum_{k=0}^n\binom nkd_k
$$

但是这个式子带 $\sum$，不优雅。

$$
\begin{aligned}
d_n&=\sum_{k=0}^n(-1)^k\binom nk(n-k)!\\
&=\sum_{k=0}^n(-1)^k\frac{n!(n-k)!}{k!(n-k)!}\\
&=n!\sum_{k=0}^n\frac{(-1)^k}{k!}\\
\end{aligned}
$$

对 $e^{-1}$ 泰勒展开。

$$
e^{-1}=\sum_{k=0}^\infty\frac{(-1)^k}{k!}
$$

那么 $e^{-1}n!-d_n$ 就可以计算了。

$$
\begin{aligned}
&e^{-1}n!-d_n\\
&=n!(\sum_{k=0}^\infty\frac{(-1)^k}{k!}-\sum_{k=0}^n\frac{(-1)^k}{k!})\\
&=n!\sum_{k=n+1}^\infty\frac{(-1)^k}{k!}\\
&=n!\sum_{k=0}^\infty\frac{(-1)^{n+k+1}}{(n+k+1)!}\\
&=(-1)^{n+1}n!\sum_{k=0}^\infty\frac{(-1)^k}{(n+k+1)!}\\
&=(-1)^{n+1}\sum_{k=0}^\infty(-1)^k\frac{n!}{(n+k+1)!}\\
\end{aligned}
$$

对于 $i$ 为奇数，有：

$$
0<\frac{n!}{(n+i)!}-\frac{n!}{(n+i+1)!}<\frac{n!}{(n+i)!}<\frac1{n^i}
$$

$$
0<\sum_{k=0}^\infty(-1)^k\frac{n!}{(n+k+1)!}<\sum_{i=0}^\infty\frac1{n^{2i+1}}=\frac n{n^2-1}
$$

所以把这个式子带入

$$
\begin{aligned}
0<\sum_{k=0}^\infty(-1)^k\frac{n!}{(n+k+1)!}<\frac n{n^2-1}\\
0<|(-1)^{n+1}\sum_{k=0}^\infty(-1)^k\frac{n!}{(n+k+1)!}|<(-1)^{n+1}\frac n{n^2-1}\\
0<|e^{-1}n!-d_n|<\frac n{n^2-1}\\
\end{aligned}
$$

当 $n\ge3$ 时，$\frac n{n^2-1}<\frac12$ 成立，所以 $0<|e^{-1}n!-d_n|<\frac12$。  
当 $n=1$ 或 $n=2$ 时，$0<|e^{-1}n!-d_n|<\frac12$ 经计算，也成立。  
所以 $d_n$ 就是 $e^{-1}n!$ 四舍五入，也就是 $\lfloor e^{-1}n!+\frac12\rfloor$。  
由此，还可以知道 $\lim\limits_{n\to\infty}\frac{d_n}n=\frac1e$。  