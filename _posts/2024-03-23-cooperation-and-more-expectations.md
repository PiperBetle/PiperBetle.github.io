---
layout: post
title: "随机策略下合作能获得更多期望"
tags: 科普 数学
---

$m+2$ 个人进行游戏。随机抛一枚均匀硬币 $n$ 次（$n$ 为奇数），每个人都要作出 $n$ 次猜测正反。猜对次数最多的那些人会平分 $m+2$ 元。若无人猜对任何一次，则无人获奖。  
由于正反均匀，所以 $m$ 个人均采取随机猜测。但是，有两人决定合作。他们的策略是其中一人随机猜测，另外一人的每次猜测都与他相反。最后，这两个人将获得 $X$ 元，求 $\mathbb E[X]$。

---

为了解决这一个问题，先去看另一个弱化版。  
$n+1$ 个人进行游戏，每个人有 $p$ 概率赢。赢的那些人会平分 $1$ 元。若无人赢，则无人获奖。  
首先，无人获奖代表所有人都输了。得到总获奖期望为 $1-(1-p)^{n+1}$。  
由于游戏公平，所以每个玩家均分总获奖期望，即每个人期望得到 $\frac{1-(1-p)^{n+1}}{n+1}$。  
设变量 $X$ 表示其中一名玩家获奖的期望，那么 $\mathbb E[X]=\frac{1-(1-p)^{n+1}}{n+1}$。  
根据条件期望，$p\mathbb E[X\vert \text 赢]+(1-p)\mathbb E[X\vert 输]=\mathbb E[X]$，显然 $\mathbb E[X\vert 输]=0$，解得 $\mathbb E[X\vert \text 赢]=\frac{1-(1-p)^{n+1}}{(n+1)p}$。  
注意如果已知一名玩家获胜，那么剩下的玩家符合参数为 $(n,p)$ 的二项随机变量 $B$，此时 $B+1$ 同时平分这 $1$ 元，即 $\mathbb E[X\vert \text 赢]=\mathbb E[\frac1{1+B}]$。

$$
\mathbb E[\frac1{B+1}]=\sum_{i=0}^n\frac{\binom nip^i(1-p)^{n-i}}{i+1}=\frac{1-(1-p)^{n+1}}{(n+1)p}
$$

---

回到原问题，显然，合作的两人中，有且仅有一人的答对数量超过 $\frac n2$。  
对于其他人，由于对于每次答对的的概率和答错的概率相等，而答对数不可能等于答错数（因为 $n$ 是奇数），所以答对超过 $\frac n2$ 的概率就是 $\frac12$。即其他 $m$ 个人答对数量超过 $\frac n2$ 的人数为参数是 $(m,\frac12)$ 的二项随机变量 $B$。  
只有答对数量超过 $\frac n2$ 的人才可能平分 $m+2$ 元，所以一共有 $B+1$ 人有可能平分 $m+2$ 元。  
由于游戏公平，这 $B+1$ 人平分 $m+2$ 元，如果设合作者一共获得 $X$ 元，那么

$$
\mathbb E[X]=\mathbb E[\frac{m+2}{B+1}]=(m+2)\mathbb E[\frac1{B+1}]
$$

我们在上面已经算出 $\mathbb E[\frac1{B+1}]$ 了，带入

$$
\begin{aligned}
\mathbb E[X]&=(m+2)\frac{1-(\frac12)^{m+1}}{(m+1)\frac12}=\frac{2(m+2)}{(m+1)}(1-(\frac12)^{m+1})\\
&=-\frac{2^{-m}m}{m+1}+\frac{2 m}{m+1}-\frac{2^{1-m}}{m+1}+\frac{4}{m+1}\\
&=2+\frac2{m+1}-\frac{2^{-m} m}{m+1}-\frac{2^{1-m}}{m+1}\\
&>2
\end{aligned}
$$

也就是说，合作能够带来更大的期望。

---

要是有 $m+4$ 人，其中 $4$ 个人选择了合作，组成两队呢？  
类似的，得去计算 $\mathbb E[\frac1{B+2}]$，仍然采取条件概率去钦定两个人赢，$B$ 是参数为 $(n,p)$ 的二项随机变量。

$$
\sum_{i=1}^k\binom kip^k(1-p)^{k-i}i\mathbb E[\frac1{B+i}]=k\frac{1-(1-p)^{n+1}}{n+k}
$$

带入 $k=2$，$\mathbb E[\frac1{B+1}]$ 去解 $\mathbb E[\frac1{B+2}]$。

$$
\mathbb E[\frac1{B+1}]=\frac{1-(1-p)^{n+1}}{(n+1)p}
$$

```mma
eb1 = (1 - (1 - p)^(n + 1))/(n + 1)/p
Solve[2 p (1 - p) eb1 + 2 p^2 eb2 == 
  2 (1 - (1 - p)^(n + 1))/(n + 2), {eb2}]
```

$$
\mathbb E[\frac1{B+2}]=\frac{(n p+2 p-1) \left(p (1-p)^n-(1-p)^n+1\right)}{(n+1) (n+2) p^2}
$$

记 $X$ 为其中一对合作者获得的钱。

$$
\begin{aligned}
\mathbb E[X]=\frac{2m(m+4)}{(m+1)(m+2)}((\frac12)^m+1)>2
\end{aligned}
$$

也就是说，有两队合作时，合作仍然能够带来更大的期望。