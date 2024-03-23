---
layout: post
title: "一些抽卡问题的期望"
tags: 笔记 数学
---

你正在玩神原，你对抽卡问题很感兴趣。  
有 $n$ 名角色需要收集，每次随机等概率从 $n$ 名中获得一个，可能会重复获得，需要抽 $X$ 次才能全部收集 $n$ 名角色，求 $\mathbb E[X]$。

设 $X_i$ 表示已经获得 $i-1$ 名角色，要收集第 $i$ 名角色的抽卡数量，根据期望的可加性得到 $\mathbb E[X]=\sum\limits_{i=1}^n\mathbb E[X_i]$。  
在收集第 $i$ 名角色时，有 $\frac{i-1}n$ 概率获得重复角色，$\frac{n-i+1}n$ 概率获得新角色，并且结束当前阶段抽卡。  
所以说，$X_i$ 是参数为 $(\frac{n-i+1}n)$ 的几何随机变量，其期望为 $\frac n{n-i+1}$。

$$
\mathbb E[X]=\sum_{i=1}^n\mathbb E[X_i]=\sum_{i=1}^n\frac n{n-i+1}=\sum_{i=1}^n\frac ni=n\sum_{i=1}^n\frac1i
$$

但是要是角色是不等概率获取，第 $i$ 名角色抽到的概率为 $p_i$（$\sum p_i=1$），那么 $\mathbb E[X]$ 如何计算呢？

设 $X_i$ 表示收集到第 $i$ 名角色时的累计抽卡数量，那么 $X=\max\limits_{i=1}^nX_i$。  
$X_i$ 是参数为 $(p_i)$ 的几何随机变量，$\min(X_i,X_j)$ 是参数为 $(p_i+p_j)$ 的几何随机变量，$\min(X_i,X_j,X_k)$ 是参数为 $(p_i+p_j+p_k)$ 的几何随机变量，那不妨进行一个 min-max 容斥？

$$
\mathbb E[X]=\sum_{i}\frac1{p_i}-\sum_{i}\sum_{i<j}\frac1{p_i+p_j}+\sum_{i}\sum_{i<j}\sum_{j<k}\frac1{p_i+p_j+p_k}-\cdots+(-1)^{n+1}\frac1{p_1+p_2+\cdots+p_n}
$$

不好了，粉球不够了，只剩下 $m$ 个，其他条件不变，记 $m$ 抽获得的角色数量为 $X$，求 $\mathbb E[X]$ 和 $Var(X)$。

记 $A_i$ 表示 $m$ 抽后没有 $i$ 号角色的概率，那么 $\mathbb p(A_i)=(1-p_i)^m$。

$$
\mathbb E[1-X]=\sum_{i=1}^n(1-p_i)^n
$$

类似的，$\mathbb E[A_iA_j]=(1-p_i-p_j)^m$。

$$
\mathbb E[X(X-1)]=2\sum_i\sum_{i<j}\mathbb P(A_iA_j)=2\sum_i\sum_{i<j}(1-p_i-p_j)^m\\
Var(X)=Var(1-X)=2\sum_i\sum_{i<j}(1-p_i-p_j)^m+\sum_{i=1}^n(1-p_i)^n-(\sum_{i=1}^n(1-p_i)^n)^2
$$

那要是在等概率下，获得所有角色后，零命角色数量为 $X$，求 $\mathbb E[X]$ 和 $Var(X)$。

记 $A_i$ 表示收集到的第 $i$ 个角色在结束时是否为零命，那么 $\mathbb E[X]=\sum\limits_{i=1}^n\mathbb P(A_i)$。
当抽到第 $i$ 个角色时，之后还有 $n-i$ 个角色需要抽取。如果把这 $n-i$ 个角色和第 $i$ 个 角色下一次出现排成一个序列，那么当且仅当角色 $i$ 在最后一位时，能够做到结束游戏并且 $i$ 仍然零命。  
由于等概率，所以 $\mathbb P(A_i)$ 就是 $i$ 在其他 $n-i$ 个角色后面的概率，即 $\frac1{n-i+1}$。

$$
\mathbb E[X]=\sum_{i=1}^n\frac1{n-i+1}=\sum_{i=1}^n\frac1i
$$

记 $S_{i,j}$ 表示收集到第 $j$ 个角色时，第 $i$ 个角色零命的概率。  
类似的，抽到第 $i$ 个角色时，之后还有 $n-i$ 个角色需要抽取。如果把这 $n-i$ 个角色和第 $i$ 个 角色下一次出现排成一个序列，那么当且仅当角色 $i$ 不在前 $j-i$ 个时，$S_{i,j}$ 成立。  
由于等概率，所以 $\mathbb P(S_{i,j})=\frac{n+1-j}{n+1-i}$。

接下来需要计算 $\mathbb P(A_iA_j\mid S_{i,j})$，收集到第 $i$ 个角色和第 $j$ 个角色后，要使 $A_i$ 和 $A_j$ 都发生。  
如果把 $i$，$j$ 和剩余 $n-j$ 个角色下一次出现排成一个序列，那么当且仅当角色 $i$ 和角色 $j$ 在最后时，$A_iA_j$ 成立。  
由于等概率，所以 $\mathbb P(A_iA_j\mid S_{i,j})=\frac2{(n-j+1)(n-j+2)}$。

$$
\mathbb P(A_iA_j)=\mathbb P(A_iA_j\mid S_{i,j})\mathbb P(S_{i,j})=\frac2{(n-i+1)(n-j+2)}\\
\mathbb E[X(X-1)]=4\sum_i\sum_{i<j}\frac1{(n-i+1)(n-j+2)}\\
Var(X)=4\sum_i\sum_{i<j}\frac1{(n-i+1)(n-j+2)}+\sum_{i=1}^n\frac1i-(\sum_{i=1}^n\frac1i)^2
$$