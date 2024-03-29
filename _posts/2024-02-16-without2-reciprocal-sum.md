---
layout: post
title: "所有十进制数位中不含2的正整数的倒数和"
tags: 笔记 数学
---

$x\ge1$，首先证明个简单的引理：

$$
\frac1x>\frac9{10}(\sum_{i=0}^9\frac1{10x+i}-\frac1{10x+2})
$$

不妨设

$$
f(x)=\frac1x((\sum\limits_{i=0}^9\frac1{10x+i})-\frac1{10x+2})\\
f(x)=\frac{4536 + 211284 x + 2812995 x^2 + 17430700 x^3 + 59386250 x^4 +  118230000 x^5 + 137200000 x^6 + 86000000 x^7 + 22500000 x^8}{45360 + 1056420 x + 9376650 x^2 + 43576750 x^3 + 118772500 x^4 + 
 197050000 x^5 + 196000000 x^6 + 107500000 x^7 + 25000000 x^8}\\
$$

上下最高次数都是 $8$，并且都是 $\frac\infty\infty$ 的形式，所以洛必达上下各求 $8$ 次导。另外 $1$ 次导为正，可以判断单调递增。

$$
\lim_{x\to\infty}f(x)=\frac{907200000000}{1008000000000}=\frac9{10}
$$

还有个更简单的证明方式：

$$
\frac1x>\frac9{10x}>\frac9{10}(\sum_{i=0}^9\frac1{10x+i}-\frac1{10x+2})
$$

当 $x$ 为一位数时，$10x+0,10x+1,10x+3,\cdots,10x+9$ 正好包含了所有 $1$ 开头不含 $2$ 的二位数，并且它们的倒数和小于 $\frac1x$ 的 $\frac9{10}$。  
再对 $10x+0,10x+1,10x+3,\cdots,10x+9$ 进行扩展，正好包含了所有 $1$ 开头不含 $2$ 的三位数，并且它们的倒数和小于 $\frac1x$ 的 $(\frac9{10})^2$。  
所以对于所有一位数 $x$，以其为前缀的 $i$ 位数倒数和小于 $(\frac9{10})^{i-1}$。  
那么所有不含 $2$ 的正整数的倒数和，就可以分类为 $d(d=1,3,4,\ldots,9)$ 开头的不含 $2$ 的正整数的倒数和，并且 $i$ 位的倒数和小于 $i-1$ 位的 $\frac9{10}$。

所以

$$
\begin{aligned}
S&<(\sum_{i=1}^9-\frac12)+(\sum_{i=1}^9-\frac12)\frac9{10}+(\sum_{i=1}^9-\frac12)(\frac9{10})^2+\ldots\\
&=(\sum_{i=1}^9-\frac12)(1+\frac9{10}+(\frac9{10})^2+\ldots)\\
&=\frac{5869}{2520}\times\frac1{1-\frac9{10}}\\
&=\frac{5869}{252}\\
&\lesssim23.2897
\end{aligned}
$$

这样就得到了一个比较松的上界。  
把 $[100000,999999]$ 开头的算出来，再加上 $[1,99999]$ 符合条件的，可以再紧一些，不到 $19.2574$。

```mma
Sum[If[StringContainsQ[ToString[i],"2"],0,1/i],{i,1,99999}]+Sum[If[StringContainsQ[ToString[i],"2"],0,1/i],{i,100000,999999}]*1/(1-9/10)//N
```