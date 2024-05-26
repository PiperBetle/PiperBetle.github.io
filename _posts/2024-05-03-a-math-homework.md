---
layout: post
title: "随机作业20240503"
tags: 数学
---

$f(x)=a\ln x-x+b$。若 $f(x)\ge kx-x\ln x-a$ 对 $\forall a\in[1,2],x\in[1,\mathrm e]$ 恒成立，则记最大的 $k$ 为 $c$。当 $b\in[1,2]$ 时，求 $b+c$ 取值范围。

$$
k\le\frac{f(x)+x\ln x+a}x=\frac{a\ln x-x+b+x\ln x+a}x\\
c=\left(\frac{a\ln x-x+b+x\ln x+a}x\right)_{\min}=g(x)\\\ge\frac{\ln x-x+b+x\ln x+1}x=h(x)\\
h'(x)=\frac{-b+x-\ln x}{x^2}\\
p(x)=-b+x-\ln x\\
p'(x)=-\frac1x+1\ge0,p(x)\uparrow\\
p(1)=1-b,p(\mathrm e)=-1-b+\mathrm e
$$

若 $b=1$

$$
h'(x)\ge0,h(x)\uparrow\\
c=h_{\min}(x)=h(1)=b\\
b+c=2
$$

若 $2\ge b\ge\mathrm e-1$

$$
h'(x)\le0,h(x)\downarrow\\
c=h_{\min}(x)=h(\mathrm e)=\frac{2+b}{\mathrm e}\\
b+c=b+\frac{2+b}{\mathrm e}=(1+\frac1{\mathrm e})b+\frac2{\mathrm e}\\
(1+\frac1{\mathrm e})(e-1)+\frac2{\mathrm e}\le b+c\le2(1+\frac1{\mathrm e})+\frac2{\mathrm e}
$$

若 $1<b<\mathrm e-1$，记 $x_0$ 为 $h(x) $极值点，$-b+x_0-\ln x_0=0$

$$
-b+x_0-\ln x_0=0,b=x_0-\ln x_0\\
c=h_{\min}(x)=h(x_0)=\frac{\ln x_0-x_0+b+x_0\ln x_0+1}{x_0}\\
=\frac{x_0\ln x_0+1}{x_0}\\
b+c=x_0-\ln x_0+\frac{x_0\ln x_0+1}{x_0}=x_0+\frac1{x_0}\\
2<b+c<\mathrm e+\frac1{\mathrm e}
$$