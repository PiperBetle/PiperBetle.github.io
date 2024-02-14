---
layout: post
title: "对二项式定理求导"
tags: 笔记 数学
---

$$
\begin{aligned}
(x+1)^n&=\sum_{i=0}^n\binom nix^i\\
((x+1)^n)'&=(\sum_{i=0}^n\binom nix^i)'\\
n(x+1)^{n-1}&=\sum_{i=0}^n\binom niix^{i-1}\\
2^{n-1}n&=\sum_{i=0}^ni\binom ni
\end{aligned}
$$

$$
\begin{aligned}
(x+1)^n&=\sum_{i=0}^n\binom nix^i\\
((x+1)^n)'&=(\sum_{i=0}^n\binom nix^i)'\\
n(x+1)^{n-1}&=\sum_{i=0}^n\binom niix^{i-1}\\
(n(x+1)^{n-1})'&=(\sum_{i=0}^n\binom niix^{i-1})'\\
n(n-1)(x+1)^{n-2}&=\sum_{i=0}^n\binom nii(i-1)x^{i-2}\\
n(n-1)2^{n-2}&=\sum_{i=0}^ni(i-1)\binom ni\\
n(n-1)2^{n-2}+2^{n-1}n&=\sum_{i=0}^ni(i-1)\binom ni+\sum_{i=0}^ni\binom ni\\
n(n-1)2^{n-2}+2\times2^{n-2}n&=\sum_{i=0}^ni^2\binom ni\\
n(n+1)2^{n-2}&=\sum_{i=0}^ni^2\binom ni\\
\end{aligned}
$$