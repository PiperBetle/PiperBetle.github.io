---
layout: post
title: "切比雪夫多项式"
tags: 笔记 数学
---

切比雪夫多项式的最初根源其实是从 $\cos$ 的多倍角公式，但其优秀性质却被用在了多项式绝对值最大值中的最小值。

|n|$\cos$|$T_n$|
|:-:|:-:|:-:|
|$0$|$\cos0$|$T_0=1$|
|$1$|$\cos\theta=\cos\theta$|$T_1=x$|
|$2$|$\cos2\theta=2\cos^2\theta-1$|$T_2=2x^2-1$|
|$3$|$\cos3\theta=4\cos^3\theta-3\cos\theta$|$T_3=4x^3-3x$|
|$4$|$\cos4\theta=8\cos^4\theta-8\cos^2\theta+1$|$T_4=8x^4-8x^2+1$|
|$n+1$|$\cos(n+1)\theta=2\cos\theta\cos n\theta-\cos(n-1)\theta$|$T_{n+1}=2xT_n-T_{n-1}$|


因为是 $\theta$ 的和角，所以 $T_n$ 的第 $i$ 个根是 $\cos(\frac{2i-1}{2n}\pi)$。  
同理还可以得出 $T_n$ 在 $[-1,1]$ 中有 $n+1$ 个极值点 $x_i=\cos(\frac in\pi),i\in[0,n]\cap\mathbb Z$，并且 $T_n(x_i)=(-1)^i$。


性质：首项系数为 $1$ 的 $n$ 次多项式 $f(x)$ 一定存在 $x_0\in[-1,1]$ 满足 $\vert f(x)\vert\ge\frac1{2^{n-1}}$。  
证明可以采取反证法，设 $F(x)=2^{n-1}f(x)$，那么假设 $\vert F(x)\vert<1$。  
$F(x)-T_n(x)$ 是个 $n-1$ 次的多项式，因为第 $n$ 次被抵消了。  
$x=\cos(\frac in\pi),i\in[0,n]\cap\mathbb Z$ 时，$T_n(x)$ 的取值在 $1$ 和 $-1$ 中交替变换。因为 $\vert F(x)\vert<1$，所以 $F(x)-T_n(x)$ 的符号由 $T_n$ 来决定，相邻两项的符号也交替变换，$n+1$ 个 $x_i$ 带来了 $n$ 个零点。  
$F(x)-T_n(x)$ 这个 $n-1$ 次多项式存在 $n$ 个零点，这只能说明 $F(x)=T_n(x)$ 恒成立。  
但是必然存在 $x$ 使得 $T_n=1$ 成立，但是我们已经假设 $F(x)<1$ 了，产生矛盾，假设不成立。  
带入 $T_n$，得到当 $f(x)$ 是 $T_n$ 时取等。

对上面的性质进行平移伸缩可以得到这个结论：若 $f(x)$ 为 $n$ 次多项式，其最高项为 $ax^n$，定义域为 $D$，值域为 $I$，则

$$
\min_{x\in D}\vert f(x)\vert_{\max}=\frac{\vert I\vert}2=2^{1-2n}\vert a\vert\vert D\vert^n
$$

$$
\frac{\vert I\vert}2\ge2^{1-2n}\vert a\vert\vert D\vert^n$$

取等条件为 $f(x)$ 是 $T_n(x)$ 经过平移伸缩使得定义域为 $D$ 的函数。

也就是说，一个多项式，它的值就像被它的次数和最高项系数还有定义域「下毒」了。这就是切比雪夫多项式的高妙之处，得到了这个反直觉结论。

---

$f(x)=2x^2+bx+c$，当 $x\in[0,2]$ 时，求 $\min\vert f(x)\vert_{\max}$。

$$
\begin{aligned}
\min\vert f(x)\vert_{\max}&=2^{1-2n}\vert a\vert\vert D\vert^n\\
&=2^{1-2\times2}\vert2\vert2^2\\
&=1
\end{aligned}
$$

---

$f(x)=x^2+ax+b-2$ 在 $x\in[1,3]$ 上 $\vert f(x)\vert\le\frac12$ 恒成立，求 $a,b$。

注意到 $\min\vert f(x)\vert_{\max}=2^{1-2n}\vert a\vert\vert D\vert^n=\frac12$，所以 $a,b-2$ 就是 $T_2$ 的 $1,0$ 次项系数。  
为了取等，得把 $T_2$ 的定义域右移 $2$，同时为了使最高项系数 $[x^2]T_2=2$ 与 $[x^2]f(x)=1$ 对应 还要乘 $\frac12$。  
也就是说，$f(x)=\frac12T_2(x-2)$，展开后解出 $a=-4,b=\frac{11}2$ 即可。

---

$f(x)=ax^2+bx+c$，当 $0\le x\le\frac12$ 时，$f(x)\in[2,4]$，求 $a_{\max}$。

$$
\begin{aligned}
\frac{\vert I\vert}2&\ge2^{1-2n}\vert a\vert\vert D\vert^n\\
\frac{4-2}2&\ge2^{1-2\times2}\vert a\vert(\frac12)^2\\
\vert a\vert&\le32\\
a_{\max}&=32
\end{aligned}
$$

---

$f(x)=ax^2+bx+c$，对于任意 $x\in[0,1]$ 满足 $\vert f(x)\vert\le1$，求 $\vert a\vert+\vert b\vert+\vert c\vert$ 的最大值。

$\min\vert f(x)\vert_{\max}=2^{1-2n}\vert a\vert\vert D\vert^n=\frac a8=1$，得到 $a=8$。  
然后把 $[-1,1]$ 平移伸缩到 $[0,1]$ 上，得到 $f(x)=T_2(2x-1)=8x^2-8x+1$。  
所以 $\vert a\vert+\vert b\vert+\vert c\vert$ 的最大值是 $8+8+1=19$。

---

$\vert x^2+px+q\vert\le2$ 在 $x\in[1,5]$ 上恒成立，求 $\sqrt{p^2+q^2}$ 最大值。

注意到 $\min\vert f(x)\vert_{\max}=2^{1-2n}\vert a\vert\vert D\vert^n=2$，所以 $f(x)$ 是 $T_2$ 经过平移伸缩后的函数。  
平移定义域得到 $f(x)=2T_2(\frac{x-3}2)=x^2-6x+7$，所以 $\sqrt{p^2+q^2}$ 的最大值是 $\sqrt{85}$。