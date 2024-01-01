---
layout: post
title: "线段树均摊复杂度"
tags: 技巧 题解
---

[GSS4 - Can you answer these queries IV](https://www.luogu.com.cn/problem/SP2713)
- 操作 $1$：$a_i=\sqrt{a_i},i\in[l,r]$
- 操作 $2$：询问 $\sum_{i=l}^ra_i$

开根号无法使用 tag 的方式维护，因为开根号后不确定减去多少，无法维护 $\sum a_i$。  
$a_i=2^{\log a_i}$，每次开根号后 $\log a_i$ 会减半，操作 $\log\log a_i$ 后 $\log a_i=1$，也就是说 $a_i$ 不会再发生变化了。  
$\Phi=\sum_{i=1}^n\log\log a_i$，每次区间开根都让 $\Phi$ 减少 $r-l+1$，所以开根操作的总复杂度为 $\mathcal O(n\log^2w)$。  
复杂度是 $\mathcal O(n\log^2w+q\log n)$。

[基础数据结构练习题](https://uoj.ac/problem/228)
- 操作 $1$：$a_i=a_i+x,i\in[l,r]$
- 操作 $2$：$a_i=\sqrt{a_i},i\in[l,r]$
- 操作 $3$：询问 $\sum_{i=l}^ra_i$

对于开方操作于上一题的操作不一样，修改会加上值。  
把 $a_i=\sqrt{a_i}$ 的操作变成 $a_i=a_i-(a_i-\sqrt{a_i})$，对于所有相同的值就可以一起操作了。  
而且，不仅仅是 $\min_{i=l}^r=\max_{i=l}^r$ 可以进行操作，只要满足 $\min-\sqrt{\min}=\max-\sqrt{\max}$ 就可以把开根号变成减法。那么把线段 $s$ 变为完全相同的次数就是 $\mathcal O(\log\log(\max-\min))$。  
$\Phi=\sum_s\log\log(\max-\min)$，每次区间加只会让 $\log n$ 块势能增加 $\log\log w$。  
复杂度是 $\mathcal O(q\log n\log\log w)$。

[I like Query Problem](https://atcoder.jp/contests/abc256/tasks/abc256_h)
- 操作 $1$：$a_i=\lfloor\frac{a_i}x\rfloor,i\in[l,r]$
- 操作 $2$：$a_i=x,i\in[l,r]$
- 操作 $3$：询问 $\sum_{i=l}^ra_i$

同理，对每个线段 $s$ 维护 $\min,\max$。如果区间内 $\min=\max$ 就直接整除，否则就暴力除最多 $\log w$ 次。推平就打标记。  
$\Phi=\sum_s\log(\max-\min)$，每次区间推平只会让 $\log n$ 块势能增加 $\log w$。  
复杂度是 $\mathcal O(q\log n\log w)$。

[And RMQ](https://codeforces.com/gym/103107/problem/A)
- 操作 $1$：$a_i=a_i\space\&\space x$
- 操作 $2$：$a_i=x$
- 操作 $3$：询问 $\max_{i=l}^r$

对于操作 $1$ 暴力操作。记录每个线段的 $\operatorname{or}_s$，若 $\operatorname{or}_s\&\space x=0$ 就直接不对这条线段进行操作。  
$\Phi=\sum_s\operatorname{popcnt}(\operatorname{or}_s)$。初始时 $\Phi=n\log w$。操作 $1$ 遍历过得每个节点都至少让 $\Phi$ 减少 $1$。操作 $2$ 会让 $\Phi$ 增加 $\log n\log w$。所以总势能最多为 $n\log w+q\log w$。  
复杂度是 $\mathcal O(n\log w+q\log n
\log w+n\log n)$。

[Counting Stars](https://acm.hdu.edu.cn/showproblem.php?pid=7059)
- 操作 $1$：$a_i=a_i+\operatorname{highbit}(a_i),i\in[l,r]$
- 操作 $2$：$a_i=a_i-\operatorname{lowbit}(a_i),i\in[l,r]$
- 操作 $3$：询问 $\sum_{i=l}^ra_i$，对 $998244353$ 取模

发现无论怎么操作，$\operatorname{popcnt}(a_i)$ 总是不升的。记录最高位，如果是操作 $1$ 就相当于 $a_i=a_i+2^{\operatorname{highbit}(a_i)}$，只储存 $2^{\operatorname{highbit}}$ 的话就是区间乘 $2$。如果是操作 $2$ 就可以暴力修改，修改完顺便维护一下最高位有没有被减掉，区间是否全 $0$。  
$\Phi=\sum_{i=1}^n\operatorname{popcnt}(a_i)$。  
复杂度是 $\mathcal O(n\log w+n\log n)$。

[Lowbit](https://acm.hdu.edu.cn/showproblem.php?pid=7116)
- 操作 $1$：$a_i=a_i+\operatorname{lowbit}(a_i),i\in[l,r]$
- 操作 $2$：询问 $\sum_{i=l}^ra_i$，对 $998244353$ 取模

做法几乎差不多。一个数在执行 $\log w$ 次后必然仅有最高位为 $1$。这个时候操作 $1$ 就为区间乘 $2$ 了。  
$\Phi=\sum_{i=1}^n\log(a_i)$（这里的 $a_i$ 是原始序列）。  
复杂度是 $\mathcal O(n\log w+n\log n)$。

[Gorgeous Sequence](https://acm.hdu.edu.cn/showproblem.php?pid=5306)
- 操作 $1$：$a_i=\max(a_i,x),i\in[l,r]$
- 操作 $2$：询问 $\max_{i=l}^r$
- 操作 $3$：询问 $\sum_{i=l}^ra_i$

维护区间最小值 $mn_1$，最小值出现次数 $cnt$，严格次小值 $mn_2$。如果 $x\le mn_1$ 直接退出。如果 $mn_2<x\le mn_1$ 就用 $x$ 更新 $mn_1$ 和 $cnt$ 等。否则递归儿子。  
由于我太菜了，所以证明在[这里](https://charleswu.site/wp-content/uploads/2023/01/%E5%90%89%E5%A6%82%E4%B8%80-%E5%8C%BA%E9%97%B4%E6%9C%80%E5%80%BC%E6%93%8D%E4%BD%9C%E4%B8%8E%E5%8E%86%E5%8F%B2%E6%9E%81%E5%80%BC%E9%97%AE%E9%A2%98.pdf)。  
复杂度是 $\mathcal O(n\log^2n)$。

---
关于 Beats，等我彻底理解了再继续写。