---
layout: post
title: "裂项 TRICK"
tags: 笔记 数学
---

$$
\begin{aligned}
\frac1{n^\frac12}&=\frac{2}{\sqrt n+\sqrt n}\\
&<\frac{2}{\sqrt{n-1}+\sqrt n}\\
&=2(-\sqrt{n-1}+\sqrt n)
\end{aligned}
$$

$$
\begin{aligned}
\frac1{n^\frac32}&<\frac{\sqrt n}{\sqrt n\sqrt n\sqrt{n+1}\sqrt{n-1}}\\
&=\frac{\frac{\sqrt{n+1} \sqrt{n}-\sqrt{n} \sqrt{n-1}}{\sqrt{n+1}-\sqrt{n-1}}}{\sqrt n\sqrt n\sqrt{n+1}\sqrt{n-1}}\\
&=(\frac1{\sqrt n\sqrt{n-1}}-\frac1{\sqrt n\sqrt{n+1}})\frac1{\sqrt{n+1}-\sqrt{n-1}}\\
&=(\frac1{\sqrt{n-1}}-\frac1{\sqrt{n+1}})(\frac{\sqrt{n+1}+\sqrt{n-1}}{2\sqrt n})\\
&<\frac1{\sqrt{n-1}}-\frac1{\sqrt{n+1}}
\end{aligned}
$$

$$
\begin{aligned}
\frac1{\binom nm}-\frac1{\binom{n+1}m}&=\frac{\binom{n+1}m-\binom nm}{\binom nm\binom{n+1}m}\\
&=\frac{\binom n{m-1}}{\binom nm\binom{n+1}m}\\
&=\frac{m}{(n+1)\binom nm}\\
&=\frac{m}{(m+1)\binom{n+1}{m+1}}\\
\end{aligned}
$$