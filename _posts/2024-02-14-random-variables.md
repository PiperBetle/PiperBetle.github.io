---
layout: post
title: "随机变量，以及它们的期望和方差"
tags: 笔记 数学
---

# 前置知识
期望 $E[X]$ 即概率的加权平均。  
期望具有线性，$E[ax+b]=aE[x]+b$。  
方差 $Var(x)=E[X^2]-E^2[x]$。  
类似的，$Var(ax+b)=a^2Var(x)$。
# 二项随机变量
## 定义
进行 $n$ 次独立事件，每次成功的概率为 $p$，失败的概率为 $1-p$，那么成功 $i$ 次的变量叫做**二项随机变量**，其参数为 $(n,p)$，其分布列为：

$$
p(i)=\binom nip^i(1-p)^{n-i},i\ge0
$$

「运气轮」游戏：闲家从 $[1,6]$ 选 $1$ 个数字。庄家扔 $3$ 枚骰子，如果选取的数字出现了 $i(1\le i\le3)$ 次，则闲家从庄家赢取 $i$ 摩拉，否则庄家从闲家赢取 $1$ 摩拉。  
设 $X$ 为闲家赢取的摩拉：  

$$
P\{X=-1\}=\binom30(\frac16)^0(\frac56)^3=\frac{125}{256}\\
P\{X=1\}=\binom31(\frac16)^1(\frac56)^2=\frac{75}{256}\\
P\{X=2\}=\binom32(\frac16)^2(\frac56)^1=\frac{15}{256}\\
P\{X=3\}=\binom33(\frac16)^3(\frac56)^0=\frac1{256}\\
E[X]=\frac{-125+75+2\times15+3\times1}{216}=-\frac{17}{216}
$$
## 期望、方差

$$
\begin{aligned}
E[X^k]&=\sum_{i=0}^ni^k\binom nip^i(1-p)^{n-i}\\
&=\sum_{i=1}^ni^k\binom nip^i(1-p)^{n-i}\\
&=np\sum_{i=1}^ni^{k-1}\binom{n-1}{i-1}p^{i-1}(1-p)^{n-i}\\
&=np\sum_{i=1}^ni^{k-1}\binom{n-1}{i-1}p^{i-1}(1-p)^{n-(i-1)-1}\\
&=np\sum_{i=0}^{n-1}(i+1)^{k-1}\binom{n-1}ip^i(1-p)^{n-i-1}\\
\end{aligned}
$$

令 $Y$ 为参数 $(n-1,p)$ 的二项随机变量，得到：

$$
E[X^k]=npE[(Y+1)^{k-1}]
$$

带入 $k=1$

$$
E[X]=npE[(Y+1)^0]=np
$$

带入 $k=2$

$$
E[X^2]=npE[(Y+1)^1]=np((n-1)p+1)
$$

$$
Var(x)=np((n-1)p+1)-(np)^2=np(1-p)
$$

# 泊松随机变量
## 定义
**泊松随机变量**，其参数为 $(\lambda)$，其分布列为：

$$
p(i)=e^{-\lambda}\frac{\lambda^i}{i!},i\ge0
$$

参数为 $(n,p)$ 的二项随机变量在 $n$ 充分大，$p$ 足够小使得 $np$ 适当时，可以近似看作参数为 $\lambda=np$ 的泊松随机变量。

$$
\begin{aligned}
\binom nip^i(1-p)^{n-i}&=\binom ni(\frac\lambda n)^i(1-\frac\lambda n)^{n-i}\\
&=\frac{n^{\underline i}\lambda^i(1-\frac\lambda n)^n}{i!n^i(1-\frac\lambda n)^i}\\
&=(1-\frac\lambda n)^n\frac{\lambda^i}{i!}\frac{n^{\underline i}}{n!}(1-\frac\lambda n)^i\\
&\approx e^{-\lambda}\frac{\lambda^i}{i!}
\end{aligned}
$$

制作甜甜花酿鸡的失败率为 $0.1$，计算生产 $10$ 个甜甜花酿鸡失败次数不超过 $1$ 次的概率。  
可以运用二项随机变量，$\binom{10}0\times0.1^0+0.9^{10}+\binom{10}1\times0.1^1+0.9^9=0.7361$。  
可以用泊松随机变量求得一个近似解，$\lambda=np=0.1\times10=1$，那么 $e^{-1}(\frac{1^0}{0!}+\frac{1^1}{1!})=2e^{-1}\approx0.735759$，算出来还是很接近的。

稻妻的核废水有放射性，每秒平均放出 $3.2$ 个雷元素，计算放出的雷元素不超过 $2$ 概率的	近似值。  
设有 $n$ 个分子有放射性（$n$ 足够大），那么每个分子每秒放出雷元素的概率为 $\frac{3.2}n$，那么 $\lambda=3.2$。  
用泊松随机变量，$e^{-3.2}(\frac{3.2^0}{0!}+\frac{3.2^1}{1!}+\frac{3.2^2}{2!})\approx0.379904$。

有 $n$ 个人，那么有 $\binom n2$ 个无序二元组关系，其中两个人生日相等的概率为 $\frac1{365}$，所以 $\lambda=\binom n2\frac1{365}=\frac{n(n-1)}{730}$。  
不存在生日重合的概率就是 $\exp(-\frac{n(n-1)}{730})$。  
同理，如果求不存在三个人生日相同的概率，那么 $\lambda=\binom n3(\frac1{365})^2$，不存在三个人生日重合的概率就是 $\exp(-\binom n3(\frac1{365})^2)$。  

不过以上都是用泊松随机分布算出的近似解。实际上，只要满足各个事件发生的概率较小，并且独立（或者弱相关），就可以看作泊松随机分布。
## 期望、方差
根据二项随机变量的猜测，$E[X]=np=\lambda$，$Var(X)=np(1-p)\approx np=\lambda$，也就是说 $E[X]=Var[X]=\lambda$？确实如此，接下来证明。

$$
\begin{aligned}
E[X]&=\sum_{i=0}^\infty\frac{ie^{-\lambda}\lambda^i}{i!}\\
&=\sum_{i=1}^\infty\frac{ie^{-\lambda}\lambda^i}{i!}\\
&=\lambda\sum_{i=1}^\infty\frac{e^{-\lambda}\lambda^{i-1}}{(i-1)!}\\
&=\lambda\sum_{i=0}^\infty\frac{e^{-\lambda}\lambda^i}{i!}\\
&=\lambda e^{-\lambda}\sum_{i=0}^\infty\frac{\lambda^i}{i!}\\
&=\lambda e^{-\lambda}e^\lambda\\
&=\lambda
\end{aligned}
$$


$$
\begin{aligned}
E[X^2]&=\sum_{i=0}^\infty\frac{i^2e^{-\lambda}\lambda^i}{i!}\\
&=\sum_{i=1}^\infty\frac{i^2e^{-\lambda}\lambda^i}{i!}\\
&=\lambda\sum_{i=1}^\infty\frac{i^2e^{-\lambda}\lambda^{i-1}}{i!}\\
&=\lambda\sum_{i=1}^\infty\frac{ie^{-\lambda}\lambda^{i-1}}{(i-1)!}\\
&=\lambda\sum_{i=0}^\infty\frac{(i+1)e^{-\lambda}\lambda^i}{i!}\\
&=\lambda(\sum_{i=0}^\infty\frac{ie^{-\lambda}\lambda^i}{i!}+\sum_{i=0}^\infty\frac{e^{-\lambda}\lambda^i}{i!})\\
&=\lambda(\lambda+1)
\end{aligned}
$$

$$
Var(X)=E[X^2]-E^2[X]=\lambda(\lambda+1)-\lambda^2=\lambda
$$
# 几何随机变量
## 定义
重复进行独立事件，每次成功的概率为 $p$，失败的概率为 $1-p$，那么第 $i$ 次时第一次成功的变量叫做**几何随机变量**，其参数为 $(p)$，其分布列为：

$$
p(i)=(1-p)^{i-1}p,i\ge r
$$

不难证明到最后成功的概率为 $1$。

$$
\sum_{i=1}^\infty(1-p)^ip=p\sum_{i=1}^\infty(1-p)^i=\frac{p}{1-(1-p)}=1
$$
## 期望、方差
记 $q=1-p$

$$
\begin{aligned}
E[X]&=\sum_{i=1}^\infty iq^{i-1}p\\
&=\sum_{i=1}^\infty(i-1+1)q^{i-1}p\\
&=\sum_{i=1}^\infty(i-1)q^{i-1}p+\sum_{i=1}^\infty q^{i-1}p\\
&=\sum_{i=0}^\infty iq^ip+1\\
&=q\sum_{i=0}^\infty iq^{i-1}p+1\\
&=qE[X]+1
\end{aligned}
$$

$$
E[X]=\frac1{1-q}=\frac1p
$$

$$
\begin{aligned}
E[X^2]&=\sum_{i=1}^\infty i^2q^{i-1}p\\
&=\sum_{i=1}^\infty(i-1+1)^2q^{i-1}p\\
&=\sum_{i=1}^\infty(i-1)^2q^{i-1}p+\sum_{i=1}^\infty2(i-1)q^{i-1}p+\sum_{i=1}^\infty q^{i-1}p\\
&=\sum_{i=0}^\infty i^2q^ip+2\sum_{i=0}^\infty iq^ip+1\\
&=qE[X^2]+2qE[X]+1
\end{aligned}
$$

$$
E[X^2]=\frac{2q+p}{p^2}=\frac{q+1}{p^2}
$$

$$
Var(X)=\frac{q+1}{p^2}-\frac1{p^2}=\frac{1-p}{p^2}
$$
# 负二项随机变量
## 定义
重复进行独立事件，每次成功的概率为 $p$，失败的概率为 $1-p$，那么第 $i$ 次后满足累计 $r$ 次成功的变量叫做**负二项随机变量**，其参数为 $(r,p)$，其分布列为：

$$
\binom{i-1}{r-1}p^r(1-p)^{n-r},i\ge1
$$

因为负二项随机变量相当于 $r$ 个几何随机变量叠加，所以其结束的概率必然为 $1$。  
参数为 $(p)$ 的几何随机变量就是参数为 $(1,p)$ 的负二项随机变量。

温迪摘花瓣，有两朵花各有 $n$ 片花瓣。每次温迪随机从一朵花上摘除一片花瓣，问他第一次试图从摘空的花上摘花瓣，另一朵花有 $k$ 片花瓣的概率。  
这个事件只会发生在第 $2n-k+1$ 次摘花瓣时，这朵花现在摘了 $n+1$ 次，满足参数为 $(n+1,\frac12)$ 的负二项随机变量，所以概率就是 $\binom{2n-k}n(\frac12)^{2n-k+1}$。

$$
\begin{aligned}
E[X^k]&=\sum_{i=r}^\infty i^k\binom{i-1}{r-1}p^r(1-p)^{i-r}\\
&=\frac rp\sum_{i=r}^\infty i^{k-1}\binom irp^{r+1}(1-p)^{i-r}\\
&=\frac rp\sum_{i=r+1}^\infty(i-1)^{k-1}\binom{i-1}rp^{r+1}(1-p)^{i-(r+1)}
\end{aligned}
$$

令 $Y$ 为参数 $(r+1,p)$ 的负二项随机变量，得到：

$$
E[X^k]=\frac rpE[(Y-1)^{k-1}]
$$

带入 $k=1$

$$
E[X]=\frac rp
$$

带入 $k=2$

$$
E[X^2]=\frac rpE[Y-1]=\frac rp(\frac{r+1}p-1)
$$

$$
Var(X)=\frac rp(\frac{r+1}p-1)-(\frac rp)^2=\frac{r(1-p)}{p^2}
$$
# 超几何随机变量
## 定义
一个罐子有 $N$ 个球，其中 $m$ 个关键球，$N-m$ 个无关球，随机不放回取出 $n$ 个球，取出的白球数叫做**超几何随机变量**，其参数为 $(n,N,m)$，其分布列为：

$$
\frac{\binom mi\binom{N-m}{n-i}}{\binom Nn},0\le i\le n
$$

当 $N,m\gg n,i$ 时，放回和不放回类似，那么这个超几何随机变量就近似于参数为 $(n,\frac mN)$ 的二项随机变量。

$$
\begin{aligned}
E[X^k]&=\sum_{i=0}^ni^k\frac{\binom mi\binom{N-m}{n-i}}{\binom Nn}\\
&=\sum_{i=1}^ni^k\frac{\binom mi\binom{N-m}{n-i}}{\binom Nn}\\
&=\frac{nm}N\sum_{i=1}^ni^{k-1}\frac{\binom{m-1}{i-1}\binom{N-m}{n-i}}{\binom{N-1}{n-1}}\\
&=\frac{nm}N\sum_{i=0}^{n-1}(i+1)^{k-1}\frac{\binom{m-1}i\binom{N-m}{n-i-1}}{\binom{N-1}{n-1}}\\
\end{aligned}
$$

令 $Y$ 为参数 $(n-1,N-1,m-1)$ 的负二项随机变量，得到：

$$
E[X^k]=\frac{nm}NE[(Y+1)^{k-1}]
$$

令 $k=1$

$$
E[X]=\frac{nm}N
$$

令 $k=2$

$$
E[X^2]=\frac{nm}NE[Y+1]=\frac{nm}N(\frac{(n-1)(m-1)}{N-1}+1)
$$

令 $p=\frac mN$

$$
Var(X)=np(1-p)(1-\frac{n-1}{N-1})
$$