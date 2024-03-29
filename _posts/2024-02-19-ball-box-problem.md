---
layout: post
title: "有无标号球盒计数问题"
tags: 笔记 数学
---

经常遇到有/无标号的 $n$ 个球放入 $m$ 个有/无标号盒，允许/不允许盒有空的方案数一类问题。  
每次遇到都算一遍未免有些不直接，搞来搞去最后搞得组合数定义都咬不准了，所以还得整理一下。

### 异球异盒可空
有标号的 $n$ 个球放入 $m$ 个有标号盒，允许盒有空的方案数。  

每个球都可以放入任意一个盒，都会导致最后的方案不同，所以方案数就是 $m^n$。

### 同球异盒非空
无标号的 $n$ 个球放入 $m$ 个有标号盒，不允许盒有空的方案数。  

插板法，$n$ 个球有 $n-1$ 个空，分成 $m$ 份，所以插 $m-1$ 个板，所以方案数就是 $\binom{n-1}{m-1}$。

### 同球异盒可空
无标号的 $n$ 个球放入 $m$ 个有标号盒，允许盒有空的方案数。  

直接借 $m$ 个球把所有盒填满，所以就是无标号的 $n+m$ 个球放入 $m$ 个有标号盒，允许盒有空的方案数 $\binom{n+m-1}{m-1}$。

### 异球同盒非空
有标号的 $n$ 个球放入 $m$ 个无标号盒，不允许盒有空的方案数。  

不妨使用 $n\brace m$ 表示有标号的 $n$ 个球放入 $m$ 个无标号盒，不允许盒有空的方案数。  
可以考虑递推，当放入新的一个有标号球时：
- 从之前的 $m$ 个盒中选取一个，即 $m{n-1\brace m}$。
- 放到一个新盒，即 $n-1\brace m-1$。

$$
{n\brace m}=m{n-1\brace m}+{n-1\brace m-1}
$$

另外也可以采取容斥原理计算 $n\brace m$，钦定 $i$ 个盒为空，另外随便放。  
除以 $m!$ 的原因是因为盒相同。

$$
{n\brace m}=\frac1{m!}\sum_{i=0}^{m-1}(-1)^i\binom mi(m-i)^n
$$

$n\brace m$ 被称为第二类斯特林数。

### 异球异盒非空
有标号的 $n$ 个球放入 $m$ 个有标号盒，不允许盒有空的方案数。  

就是第二类斯特林数下盒不同的情况，因为盒非空，所以任意两个盒都不同，方案数是 $m!{n\brace m}$。

$$
m!{n\brace m}=\sum_{i=0}^{m-1}(-1)^i\binom mi(m-i)^n
$$

### 异球同盒可空
有标号的 $n$ 个球放入 $m$ 个无标号盒，允许盒有空的方案数。  

去枚举有 $i$ 个盒不为空的情况，方案数是 $\sum\limits_{i=1}^m{n\brace i}$。

### 同球同盒非空
无标号的 $n$ 个球放入 $m$ 个无标号盒，不允许盒有空的方案数。 

不妨使用 $p(n,m)$ 表示无标号的 $n$ 个球放入 $m$ 个无标号盒，不允许盒有空的方案数。  
先给每个盒放一个球，剩余 $n-m$ 个球可以任意放在 $m$ 个盒中，可为空。  
钦定 $i$ 个为空，就可以跑 dp：

$$
p(n,m)=\sum_{i=0}^mp(n-m,i)\\
p(n-1,m-1)=\sum_{i=0}^{m-1}p(n-m,i)\\
$$

两式相减即得递推式子 $p(n,m)=p(n-1,m-1)+p(n-m,m)$。

$p(n,k)$ 被成为 $k$ 部分拆数。若无 $k$ 的限制，被成为分拆数 $p(n)=\sum\limits_{i=1}^np(n,i)$。

### 同球同盒可空
无标号的 $n$ 个球放入 $m$ 个无标号盒，允许盒有空的方案数。

类似的，枚举 $i$ 个盒不为空的情况，方案数是 $\sum\limits_{i=1}^mp(n,i)$。