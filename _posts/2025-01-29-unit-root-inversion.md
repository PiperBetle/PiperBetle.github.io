---
layout: post
title: "单位根反演"
tags: 笔记 数学
---

### 单位根定义

$$
x^n=1
$$

在复数上的 $n$ 个根成为 $n$ 的单位根，记作 $\omega_n^0,\omega_n^1,\omega_n^2,\cdots,\omega_n^{n-1}$。$\omega_n$ 上面的指数真的是一个指数吗？我们先暂时把这个当作一个记号，不认为这是一个指数，但在后面我们会证明这的确是一个指数。  
其中 $\omega_n^0=1$，是一个平凡单位根。  
我们知道，复数可以用向量表示。具体地说，复数 $a+b\mathrm i$ 可以使用向量 $(a,b)$ 来表示。  
为了方便在坐标轴上画出这个向量，我们用原点 $(0,0)$ 作为向量的起点。那么复数 $\omega_n^0=1+0\mathrm i$ 就是坐标轴上 $(0,0)$ 指向 $(1,0)$ 的向量。  

复数 $z=a+b\mathrm i$ 可以表示成三角形式 $r(\cos\theta+\mathrm i\sin\theta)$，其中 $r=\sqrt{a^2+b^2}$ 为复数 $z$ 的模长，即 $\vert z\vert$。  
采用复数的三角形式可以方便地表示复数的乘法。具体地说，$z_1=r_1(\cos\theta_1+\mathrm i\sin\theta_1),z_2=r_2(\cos\theta_2+\mathrm i\sin\theta_2)$，那么 $z_1z_2=r_1r_2(\cos(\theta_1+\theta_2)+\mathrm i\sin(\theta_1+\theta_2))$，这个可以直接展开用和角定理来证明。  
借此，我们可以用复数来表示向量的旋转。如果有向量 $\vec v=(a,b)$，其对应的复数 $z_1=a+b\mathrm i$，如果我们取一个模长为 $1$ 的复数 $z_2=\cos\theta+\mathrm i\sin\theta$，那么 $z_1z_2$ 对应的向量就是 $\vec v$ 绕原点逆时针旋转 $\theta$ 后的向量。

现在我们把 $n$ 的一个单位根 $\omega_n^t$ 的三角函数 $r(\cos\theta+\mathrm i\sin\theta)$ 写出。那么 $(\omega_n^t)^n=r^n(\cos n\theta+\mathrm i\sin n\theta)=1$。  
由于 $\vert(\omega_n^t)^n\vert=1$，并且 $r$ 是非负实数，所以 $r=1,z=\cos\theta+\mathrm i\sin\theta$。  
$\cos n\theta$ 是实数，$\mathrm i\sin n\theta$ 是纯虚数，$1$ 是实数。所以 $\cos n\theta=1,\sin n\theta=0$，也就是说 $\theta=2k\mathrm\pi/n$。  

举个例子，当 $n=3$ 时，我们取 $k=0,1,2$，那么 $\theta_0=0,\theta_1=2\pi/3,\theta_2=4\pi/3$。  
我们只取前 $n$ 个，因为 $\theta_3=\theta_0\pmod{2\pi}$，所以 $\cos\theta_0+\mathrm i\sin\theta_0=\cos\theta_3+\mathrm i\sin\theta_3$，这是同一个单位根。  
于是我们就可以写出 $\omega_3^0,\omega_3^1,\omega_3^2$

$$
\omega_3^0=1\\
\omega_3^1=-\frac12+\frac{\sqrt3}2\mathrm i\\
\omega_3^2=-\frac12-\frac{\sqrt3}2\mathrm i
$$

我们可以看出，$n$ 的单位根中，相邻两个在坐标轴上要相差 $2\pi/n$ 的弧度。  
因此单位根具有周期性，即 $\omega_n^k=\omega_n^{n+k}$。

$\omega_n^0=1$ 是 $n$ 的一个平凡单位根。$\omega_n^1$ 是最常用的一个单位根。之后每个单位根为前一个单位根逆时针旋转 $2\pi/n$ 弧度。  
由于复数乘法表示旋转，所以 $\omega_n^{k+1}=\omega_n^k\omega_n^1$。  
到这里，我们才知道 $\omega_n$ 上面的指数 $k$ 真的是一个指数。  
为了使读者方便观察 $n$ 的单位根，这里给出一段 mma 的画单位根的代码

```mma
n=3
Graphics[
 Table[Arrow[{ {0, 0}, {Re[Solve[x^n == 1, x][[i, 1, 2]]], 
     Im[Solve[x^n == 1, x][[i, 1, 2]]]} }], {i, 1, n}], Axes -> True]
```

### 单位根反演

用 $n\mid m$ 表示 $n$ 是 $m$ 的因子。  
$[n\mid m]$ 等价于 $[m\bmod n=0]$。  
$[n\nmid m]$ 等价于 $[m\bmod n\ne0]$。

$$
[m\bmod n=0]=[n\mid m]=\frac1n\sum_{k=0}^{n-1}\omega_n^{mk}
$$

证明：

$$
\begin{aligned}
\sum_{k=0}^{n-1}\omega_n^{mk}&=\sum_{k=0}^{n-1}(\omega_n^m)^k
\end{aligned}
$$

这似乎是个等比数列，公比为 $\omega_n^m$。我们需要对 $\omega_n^m$ 进行分类讨论，显然 $\omega_n^m\ne0$。

- $\omega_n^m=1$ 表示 $n$ 是 $m$ 的因子，即每一项都是 $1$，所以 $\sum$ 的和为 $n$，原式得证。
- $\omega_n^m\ne1$ 表示 $n$ 不是 $m$ 的因子，那么等比数列求和可得 $(\omega_n^{nm}-1)/(\omega_n^m-1)$。分子为 $0$ 分母不为 $0$，原式得证。

将 $m=1$ 带入单位根反演，可以得到当 $n\ge2$ 时，$n$ 的单位根和为 $0$。

$$
\sum_{k=0}^{n-1}\omega_n^k=0,n\ge2
$$

---

化简

$$
\sum_{j=0}^n\binom nj[j\bmod7=0]
$$

使用单位根反演

$$
\begin{aligned}
\sum_{j=0}^n\binom nj[j\bmod7=0]&=\sum_{j=0}^n\binom nj\frac17\sum_{k=0}^6\omega_7^{jk}\\
&=\frac17\sum_{k=0}^6\sum_{j=0}^n\binom nj\omega_7^{jk}\\
&=\frac17\sum_{k=0}^6(1+\omega_7^k)^n
\end{aligned}
$$

### 生成函数

$x^n-1$ 的因式分解

$$
\prod_{k=0}^{n-1}(x-\omega_n^k)=x^n-1
$$

将右边因式分解得到左边。  

---

试求集合 $\{1,2,\cdots,2000\}$ 有多少子集的元素和是 $5$ 的倍数。

先写出生成函数 $F(x)=(1+x)(1+x^2)\cdots(1+x^{2000})$，记 $h_n=[x^n]F(x)$，那么答案即为 $h_0+h_5+\cdots+h_{2000}$。  

如果求的不是 $5$ 的倍数而是 $2$ 的倍数，那么答案就是 $h_0+h_2+\cdots+h_{2000}$。  
我们知道带入 $x=1$ 得到的是所有偶数项系数和加上所有奇数项系数和，带入 $x=-1$ 得到的是所有偶数项系数和减去所有奇数项系数和。  
所以 $F(1)+F(-1)$ 得到的是两倍所有偶数项系数和，即 $F(1)+F(-1)=2(h_0+h_2+\cdots+h_{2000})$。  
$1$ 和 $-1$ 是 $2$ 的单位根，我们得到了 $2$ 的倍数的系数和，这引导我们去带入 $5$ 的单位根。

我们可以把这种技巧用在所有生成函数上。记

$$
F(x)=\sum_{k=0}^\infty h_kx^k
$$

记 $S$ 为 $x$ 的指数为 $d$ 的倍数的系数和，即

$$
S=\sum_{k=0}^\infty h_k[k\bmod d=0]
$$

那么

$$
S=\frac1d\sum_{j=0}^{d-1}G(\omega_d^j)
$$

证明

$$
\begin{aligned}
S&=\sum_{k=0}^\infty h_k[k\bmod d=0]\\
&=\sum_{k=0}^\infty h_k\frac1d\sum_{j=0}^{d-1}\omega_d^{jk}\\
&=\frac1d\sum_{j=0}^{d-1}\sum_{k=0}^\infty h_k\omega_d^{jk}\\
&=\frac1d\sum_{j=0}^{d-1}F(\omega_d^j)
\end{aligned}
$$

考虑带入 $x=\omega_5^0,\omega_5^1,\omega_5^2,\omega_5^3,\omega_5^4$。  

||$x^0$|$x^1$|$x^2$|$x^3$|$x^4$|
|:-:|:-:|:-:|:-:|:-:|:-:|
|$F(\omega_5^0)$|$\omega_5^0$|$\omega_5^0$|$\omega_5^0$|$\omega_5^0$|$\omega_5^0$|
|$F(\omega_5^1)$|$\omega_5^0$|$\omega_5^1$|$\omega_5^2$|$\omega_5^3$|$\omega_5^4$|
|$F(\omega_5^2)$|$\omega_5^0$|$\omega_5^2$|$\omega_5^4$|$\omega_5^1$|$\omega_5^3$|
|$F(\omega_5^3)$|$\omega_5^0$|$\omega_5^3$|$\omega_5^1$|$\omega_5^4$|$\omega_5^2$|
|$F(\omega_5^4)$|$\omega_5^0$|$\omega_5^4$|$\omega_5^3$|$\omega_5^2$|$\omega_5^1$|

我们知道 $\omega_5^0+\omega_5^1+\omega_5^2+\omega_5^3+\omega_5^4=0$，所以 $F(\omega_5^0)+F(\omega_5^1)+F(\omega_5^2)+F(\omega_5^3)+F(\omega_5^4)$ 中 $x^1,x^2,x^3,x^4$ 的系数均为 $0$。  
根据单位根的周期性，$x^6,x^7,x^8,x^9$ 这一类指数不为 $5$ 的倍数的系数均为 $0$。  
而只有 $x^0,x^5,\cdots,x^{2000}$ 这些项的系数被算了 $5$ 次。

$F(\omega_5^0)+F(\omega_5^1)+F(\omega_5^2)+F(\omega_5^3)+F(\omega_5^4)=5(h_0+h_5+\cdots+h_{2000})$，现在只需要计算这 $5$ 个值就可以了。

再次利用单位根的周期性

$$
F(\omega_5^k)=\prod_{k=0}^4(1+\omega_5^k)^{400},k\ne0
$$

我们在 $x^n-1$ 的因式分解中带入 $x=-1$

$$
\prod_{k=0}^4(-1-\omega_n^k)=(-1)^5-1=-2
$$

因此

$$
\prod_{k=0}^4(1+\omega_n^k)=2
$$

当 $k=0$ 时，$F(\omega_5^0)=2^{2000}$。

因此答案为

$$
\frac{2^{2000}+4\times2^{400}}5
$$

这个式子和 $\text{pólya}$ 定理求用 $2^{400}$ 种颜色染五边形，其中仅认为旋转同构的方案数一样。  
两者应该可以形成一个双射但是我想不出来，欢迎读者的想象。