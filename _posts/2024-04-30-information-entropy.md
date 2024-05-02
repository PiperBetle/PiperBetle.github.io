---
layout: post
title: "熵"
tags: 笔记 数学
---

### 熵的定义
有许多角度来理解熵，这里采用惊奇来引入。  
抛一枚硬币显示正面平平无奇，但原神单抽出金（概率为 $0.007$）就令人震惊。  
这里我们试图把事件的惊奇程度进行量化，这里使用函数 $S(x)$ 来表示，$x$ 表示事件发生的概率。

- 一个必然事件没有任何惊奇，所以定义 $S(1)=0$。
- 越是可能性小的事件惊奇越大，所以如果 $p<q$，则 $S(p)>S(q)$，即 $S(x)$ 单调递减。
- 不妨假设 $S(x)$ 是连续函数。
- 有独立事件 $A_1,A_2$，$\mathbb P(A_1)=p$，$\mathbb P(A_2)=q$。因为 $\mathbb P(A_1A_2)=pq$，所以 $A_1A_2$ 同时发生的惊奇是 $S(pq)$。如果我们先知道 $A_1$ 发生，那我们已经获得了 $S(p)$ 的惊奇。也就是说如果还我们知道 $A_2$ 发生，我们会额外获得 $S(pq)-S(p)$ 的惊奇，另外这个值应该为 $S(q)$。$S(pq)=S(p)+S(q)$。

可以证明，$S(x)=-c\log_2x$，其中 $c>0$。  
为了方便计算，取 $c=1$，也就是说 $S(x)=-\log x$，为了简化表达之后会省略底数 $2$。

---

如果 $X$ 是随机变量，有 $n$ 种不同取值，第 $i$ 种取值的概率为 $p_i$，那么就用

$$
\mathbb H[X]=-\sum_{i=1}^np_i\log p_i=\mathbb E[-\log\mathbb P(X)]
$$

来表示 $X$ 惊奇的期望（当 $p_i=0$ 时，我们认为 $p_i\log p_i=0$），也可以认为是 $X$ 的不确定程度。还可以认为是 $X$ 的信息量，这些说法在后面会有所涉及。  
我们使用熵来表示惊奇的期望。熵的单位是比特，用英文说是 $\text{bit}$。  
注意：熵与 $X$ 的数值无关，只取决于 $X$ 在值上的概率分布，这和期望、方差是不同的。

---

如果 $X$ 是 $01$ 随机变量，取 $1$ 的概率是 $p$，那么记

$$
\mathbb H(p)=\mathbb H[X]=-p\log p-(1-p)\log(1-p)
$$

```mma
Plot[-p Log[2, p] - (1 - p) Log[2, 1 - p], {p, 0, 1}]
```

求导可证，$\mathbb H(p)$ 在 $p=\frac12$ 时最大，此时 $\mathbb H(p)=1$。  
也就是说，随机抛一枚硬币时，如果这枚硬币是无偏的，才能带来最大的惊奇，带来 $1\text{bit}$ 的熵。  
为了区分 $\mathbb H[X]$ 和 $\mathbb H(p)$：如果参数 $X$ 是随机变量，就采取中括号；如果参数 $p$ 是概率，就采取小括号。  
顺带一提，单抽出金的熵是 $\mathbb H(0.007)\approx0.0601724$。

---

$X,Y$ 是不一定独立的随机变量。$\mathbb H[X,Y]$ 用来表达向量 $(X,Y)$ 的熵，即 $\mathbb H[(X,Y)]$。

$$
\mathbb H[X,Y]=-\sum_{i=1}^n\sum_{j=1}^mp_{i,j}\log p_{i,j}
$$

类似条件概率，条件期望，这里给出条件熵的定义：

$$
\mathbb H[X\vert Y]=-\sum_{j=1}^m\mathbb P(Y=Y_j)\sum_{i=1}^n\mathbb P(X=X_i\vert Y=Y_j)\log\mathbb P(X=X_i\vert Y=Y_j)
$$

证明：$\mathbb H[X,Y]=\mathbb H[Y]+\mathbb H[X\vert Y]$

$$
\begin{aligned}
\mathbb H[X,Y]&=-\sum_{i=1}^n\sum_{j=1}^mp_{i,j}\log p_{i,j}\\
&=-\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_j)\log\mathbb P(X=X_i,Y=Y_j)\\
&=-\sum_{i=1}^n\sum_{j=1}^m\mathbb P(Y=Y_j)\mathbb P(X=X_i\vert Y=Y_j)\\&(\log\mathbb P(Y=Y_j)+\log\mathbb P(X=X_i\vert Y=Y_j))\\
&=-\sum_{j=1}^m\mathbb P(Y=Y_j)\log\mathbb P(Y=Y_j)\sum_{i=1}^n\mathbb P(X=X_i\vert Y=Y_j)\\&-\sum_{j=1}^m\mathbb P(Y=Y_j)\log\mathbb P(X=X_i\vert Y=Y_j)\sum_{i=1}^n\mathbb P(X=X_i\vert Y=Y_j)\\
&=-\sum_{j=1}^m\mathbb P(Y=Y_j)\log\mathbb P(Y=Y_j)\\&-\sum_{j=1}^m\mathbb P(Y=Y_j)\sum_{i=1}^n\mathbb P(X=X_i\vert Y=Y_j)\log\mathbb P(X=X_i\vert Y=Y_j)\\
&=\mathbb H[Y]+\mathbb H[X\vert Y]
\end{aligned}
$$

如果我们进行了一些观测，那么 $X$ 的熵会有所降低。  
证明：$\mathbb H[X\vert Y]\le\mathbb H[X]$

$$
\begin{aligned}
\mathbb H[X\vert Y]\le\mathbb H[X]&=-\sum_{j=1}^m\mathbb P(Y=Y_j)\sum_{i=1}^n\mathbb P(X=X_i\vert Y=Y_j)\log\mathbb P(X=X_i\vert Y=Y_j)\\+&\sum_{i=1}^n\mathbb P(X=X_i)\log\mathbb P(X=X_i)\\
&=-\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_j)\log\mathbb P(X=X_i\vert Y=Y_j)\\+&\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_j)\log\mathbb P(X=X_i)\\
&=\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_j)\log\frac{\mathbb P(X=X_i)}{\mathbb P(X=X_i\vert Y=Y_j)}\\
&\le\log\mathrm e\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_j)(\frac{\mathbb P(X=X_i)}{\mathbb P(X=X_i\vert Y=Y_j)}-1)\\
&=\log\mathrm e(\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i)\mathbb P(Y=Y_i)-\sum_{i=1}^n\sum_{j=1}^m\mathbb P(X=X_i,Y=Y_i))\\
&=0\log\mathrm e=0
\end{aligned}
$$

当且仅当所有 $\frac{\mathbb P(X=X_i)}{\mathbb P(X=X_i\vert Y=Y_j)}=1$ 时成立，此时 $X,Y$ 独立。

---

说了那么多，那么信息熵和热力学熵有什么关系呢？由于我不学物理，所以随便搬运了点：  
吉布斯熵：如果体系有 $n$ 个能级，第 $i$ 个能级的概率是 $p_i$，那么体系的熵是

$$
S=-k_{\mathrm B}\sum_{i=1}^np_i\ln p_i
$$

其中 $k_{\mathrm B}$ 是波尔兹曼常数。  
这两个的数学式子几乎一模一样，只差了个系数。别忘了 $\log_2$ 和 $\ln$ 也只差了个系数。  
至于两者有没有更深入本质的联系，我不会。

### 熵与二项式定理
若 $np$ 是 $[0,n]$ 的一个整数，那么

$$
\frac{2^{n\mathbb H(p)}}{n+1}\le\binom n{np}\le2^{n\mathbb H(p)}
$$

上界容易证明，首先由二项式定理展开

$$
\binom n{np}p^{np}(1-p)^{n-np}\le\sum_{k=0}^n\binom nkp^k(1-p)^{n-k}\le(p+1-p)^n=1
$$

因此

$$
\binom n{np}\le p^{-np}(1-p)^{np-n}=2^{-np\log p}2^{-n(1-p)\log(1-p)}=2^{n\mathbb H(p)}
$$

对于下界，我们试图证明 $2^{n\mathbb H(p)}$ 大于等于二项式展开后最大的一项。而二项式展开后最大的一项其实就是 $\binom n{np}p^{np}(1-p)^{n-np}$。  
考虑证明，设最大的那项中 $p$ 的指数是 $k$：

$$
\binom n{k-1}p^{k-1}(1-p)^{k+1}\le\binom nkp^k(1-p)^k\ge\binom n{k+1}p^{k+1}(1-p)^{k-1}
$$

解出来 $k=np$，即最大项就是 $\binom n{np}p^{np}(1-p)^{n-np}$。

$$
\binom n{np}p^{np}(1-p)^{n-np}\ge\frac1{n+1}
$$

和上面一样

$$
\binom n{np}\ge\frac{p^{-np}(1-p)^{np-n}}{n+1}=\frac{2^{n\mathbb H(p)}}{n+1}
$$

<p align="right" style="font-size:1.5rem;">■</p>

通过以上结论，我们推出 $np$ 不为整数时更一般的结论。

如果 $0\le p\le\frac12$

$$
\frac{2^{n\mathbb H(p)}}{n+1}\le\binom n{\lceil np\rceil}\\
\binom n{\lfloor np\rfloor}\le2^{n\mathbb H(p)}
$$

如果 $\frac12\le p\le1$

$$
\frac{2^{n\mathbb H(p)}}{n+1}\le\binom n{\lfloor np\rfloor}\\
\binom n{\lceil np\rceil}\le2^{n\mathbb H(p)}
$$

这个界其实并不是很松，尽管上界和下界差了整整 $n+1$ 倍，不过看在 $n$ 还在 $2$ 的指数上，压住了分母带来的影响。  
当我们抛一枚 $p>\frac12$ 的硬币时，根据马尔可夫不等式，当 $n$ 足够大时，我们知道正面朝上次数几乎总是接近 $np$。  
因此，如果我们把正反序列写出，这个序列几乎总是 $\binom n{np}\approx2^{n\mathbb H(p)}$ 中的一个。而且每个序列出现的概率大概都是

$$p^{np}(1-p)^{n-np}\approx2^{-n\mathbb H(p)}$$

所以我们可以认为正反序列的结果等概率分布在约 $2^{n\mathbb H(p)}$ 种情况中。

### 提取随机比特
上文提到熵还可以认为是信息量，也就是说，我们可以从熵中提取一些无偏比特。  
先来看随机比特的定义：  
$y$ 是比特序列。令 $\vert y\vert$ 表示比特序列的长度。提取函数 $\operatorname{Ext}(X)$ 的输入是随机变量 $X$ 的值，输出是比特序列，并且满足

$$
\mathbb P(\operatorname{Ext}(X)=y\vert\space\vert y\vert=k)=2^{-k},\mathbb P(\vert y\vert=k)>0
$$

也就是说如果我们用到了至少 $1$ 个长度为 $k$ 的比特序列，那么所有 $2^k$ 个长度为 $k$ 的比特序列都是可能的输出结果。由此，我们的任意一个长度为 $k$ 的输出都是 $0,1$ 等概率的。  
直观地来看，我们根据 $X$ 的取值情况，取出了一个无偏比特序列，获取了信息量。

比如说我们对等概率随机变量 $X\in\lbrace0,1,\cdots,7\rbrace$ 构造一个提取函数 $\operatorname{Ext}$。  
最简单的方法是直接把 $x$ 的二进制高位补齐 $0$ 凑满 $3$ 位后转为比特序列作为输出。

|输入|输出|
|:-:|:-:|
|$0$|$000$|
|$1$|$001$|
|$2$|$010$|
|$3$|$011$|
|$4$|$100$|
|$5$|$101$|
|$6$|$110$|
|$7$|$110$|

记随机变量 $Y$ 表示提取的比特数。  
对于以上情况，$\mathbb E[Y]=3\times1=3$。

那要是对 $\lbrace0,1,\cdots,11\rbrace$ 构造一个提取函数 $\operatorname{Ext}$ 呢。  
直接把 $x$ 的二进制高位补齐 $0$ 凑满 $3$ 位后转为比特序列作为输出只能处理 $0\sim7$ 了，对于 $8\sim11$ 我们可以用 $2$ 位来解决。

|输入|输出|
|:-:|:-:|
|$0\sim7$|同上表|
|$8$|$00$|
|$9$|$01$|
|$10$|$10$|
|$11$|$11$|

对于以上情况，$\mathbb E[Y]=3\times\frac8{12}+2\times\frac4{12}=\frac83$。

类似的，对于 $\lbrace0,1,\cdots,14\rbrace$

|输入|输出|
|:-:|:-:|
|$0\sim11$|同上表|
|$12$|$0$|
|$13$|$1$|
|$14$|空串|

我们为了让 $\operatorname{Ext}$ 满足提取函数的性质，只能让它输出空串了，这也是没有办法的。而且如果要 $k=4$，就得有至少 $16$ 个数，但是 $\lbrace0,1,\cdots,14\rbrace$ 只有 $15$ 个数，不能采纳。  
对于以上情况，$\mathbb E[Y]=3\times\frac8{15}+2\times\frac4{15}+\frac2{15}=\frac{34}{15}$。

---

若 $X$ 是 $\lbrace0,1,\cdots,m-1\rbrace$ 的均匀随机变量，那么存在一个提取函数 $\operatorname{Ext}$，平均至少输出 $\lfloor\mathbb H[X]\rfloor-1$ 个比特。  
还记得 $\mathbb H[X]$ 是多少吗？这里 $\mathbb H[X]=-m\times\frac1m\log\frac1m=\log m$。

直接采取构造证明。如果 $m$ 是 $2$ 的幂，直接可以采取转二进制补足 $0$ 的策略，这样能够输出 $\log m$ 个比特。  
当 $m$ 不是 $2$ 的幂时，我们把 $m$ 写成二进制的形式。若 $m$ 在二进制位 $j$ 上是 $1$，就选择 $2^j$ 个数，提取为长度为 $j$ 的比特序列。能够看出二进制位上的 $1$ 越多，这个构造方法越「亏」。  
所以 $m$ 是 $2$ 的幂 $-1$ 时，最亏，我们去证明这个时候大于等于 $\lfloor\log m\rfloor-1$ 即可。  
不妨设 $m=2\times2^t-1$，长度为 $t$ 的串有 $2^t$ 个，$t-1$ 的串有 $2^{t-1}$ 个……长度为 $0$ 的串有 $1$ 个。

$$
\sum_{i=0}^ti2^i=t2^{t+1}-2^{t+1}+2\\
\lfloor\log m\rfloor-1=t-1\\
$$

两式相减，可证其具有单调递增，不难证明恒 $\ge0$。

---

有充分大的 $n$，硬币正面的概率 $p>\frac12$，现在投掷 $n$ 枚硬币，将长度为 $n$ 的正反情况作为提取函数 $\operatorname{Ext}$ 的输入，求证：
- 存在提取函数，提取的期望比特数至少为 $(1-\delta)n\mathbb H(p)$。
- 任意提取函数，提取的期望比特数至多为 $n\mathbb H(p)$。

继续采取构造证明。  
如果 $n$ 次投掷中，正面的次数为 $j$，就有 $\binom nj$ 种可能结果，并且每种可能结果出现的概率均为 $p^j(1-p)^{n-j}$。  
我们把这 $\binom nj$ 种可能结果编号为 $0\sim\binom nj-1$，然后采取上面对 $\lbrace0,1,\cdots,\binom nj-1\rbrace$ 相同的提取方法，即二进制拆分。  
记 $B$ 为这种提取方法获得比特数，$Z$ 为正面出现的次数。

$$
\mathbb E[B]=\sum_{j=0}^n\mathbb P(Z=j)\mathbb E[B\vert Z=j]
$$

上面我们已经证明：$\mathbb E[B\vert Z=j]\ge\lfloor\log\binom nj\rfloor-1$。  
取 $\varepsilon<\min(p-\frac12,1-p)$ 为一待定的常数。由于上面那个式子难以计算，所以我们只取满足 $n(p-\varepsilon)\le j\le n(p+\varepsilon)$ 的那些 $j$，这样去计算 $\mathbb E[B]$ 的下界。

$$
\binom nj\ge\binom n{\lfloor n(p+\varepsilon)\rfloor}\ge\frac{2^{n\mathbb H(p+\varepsilon)}}{n+1}
$$

这里第二个 $\ge$ 成立在之前计算熵和二项式时已经证明了。

$$
\begin{aligned}
\mathbb E[B]&\ge\sum_{j=\lfloor np(1+\varepsilon)\rfloor}^{\lceil np(1+\varepsilon)\rceil}\mathbb P(Z=j)\mathbb E[B\vert Z=j]\\
&\ge\sum_{j=\lfloor np(1+\varepsilon)\rfloor}^{\lceil np(1+\varepsilon)\rceil}\mathbb P(Z=j)(\lfloor\log\binom nk\rfloor-1)\\
&\ge(\log\frac{2^{n\mathbb H(p+\varepsilon)}}{n+1}-2)\sum_{j=\lfloor np(1+\varepsilon)\rfloor}^{\lceil np(1+\varepsilon)\rceil}\mathbb P(Z=j)\\
&\ge(n\mathbb H(p+\varepsilon)-\log(n+1)-2)\mathbb P(\vert Z-np\vert\le\varepsilon n)
\end{aligned}
$$

由切尔诺夫界，如果 $\mu=\mathbb E[X]$，那么对于任意 $0<\lambda<1$ 有 $\mathbb E[\vert X-\mu\vert\ge\lambda\mu]\le2\exp(\frac{-\mu\lambda^2}3)$。  
因此 $\mathbb E[\vert Z-np\vert>\varepsilon n]\le2\exp(\frac{-n\varepsilon^2}{3p})$，不妨把 $\mathrm e$ 放缩成 $2$ 后带入：

$$
\mathbb E[B]\ge(n\mathbb H(p+\varepsilon)-\log(n+1)-2)(1-2^{\frac{-n\varepsilon^2}{3p}})
$$

现在，选取足够小的 $\varepsilon$，

$$
n\mathbb H(p+\varepsilon)\ge(1-\frac\delta3)n\mathbb H(p)
$$

当 $n>\frac{3p}{\varepsilon^2}\ln\frac6\delta$ 时，

$$
1-2^{\frac{-n\varepsilon^2}{3p}}\ge1-\frac\delta3
$$

然后再带回原来的式子：

$$
\begin{aligned}
\mathbb E[B]&\ge(n\mathbb H(p+\varepsilon)-\log(n+1)-2)(1-2^{\frac{-n\varepsilon^2}{3p}})\\
&\ge((1-\frac\delta3)n\mathbb H(p)-\log(n+1)-2)(1-\frac\delta3)
\end{aligned}
$$

选取足够大的 $n$ 使得 $\frac\delta3n\mathbb H(p)\ge\log(n+1)+2$

$$
\mathbb E[B]\ge((1-\frac{2\delta}3)n\mathbb H(p))(1-\frac\delta3)\ge(1-\delta)n\mathbb H(p)
$$

这样就证明完这个提取函数，提取的期望比特数至少为 $(1-\delta)n\mathbb H(p)$。  
接下来证明任意提取函数，提取的期望比特数至多为 $n\mathbb H(p)$。

先证明一个引理：如果随机变量 $X$ 的一个可能取值 $x$，$\mathbb P(X=x)=q$，那么 $\vert\operatorname{Ext}(x)\vert\le-\log q$，这是因为所有长度为 $\vert\operatorname{Ext}(x)\vert$ 比特的输出概率都是 $q$，所以 $2^{\vert\operatorname{Ext}(x)\vert}q\le1$。  
记 $B$ 为某个 $\operatorname{Ext}$ 提取的比特数，随机变量 $X$ 为 $n$ 枚硬币的结果。

$$
\begin{aligned}
\mathbb E[B]&=\sum_x\mathbb P(X=x)\vert\operatorname{Ext}(x)\vert\\
&\le-\sum_x\mathbb P(X=x)\log\mathbb P(X=x)\\
&=\mathbb H[X]\\
\end{aligned}
$$

由于每次抛硬币独立，所以 $X$ 就是每维独立的随机向量，$\mathbb H[X]=n\mathbb H(p)$。
<p align="right" style="font-size:1.5rem;">■</p>

### 编码定理
在通信中，我们经常要实现信息的发送，其中不可避免的要对信息进行打包压缩（`.tar.gz`，一点也不好笑）。  
一个离散的若干维随机向量 $\vec V$（每维是同分布随机变量）要编码为一个比特序列（就是 $0,1$ 序列），就要把 $\vec V$ 每维的可能取值编码为一个比特序列，然后把这些序列拼起来。  
为了信息的处理方便，我们规定：不存在一个取值编码为另一个取值编码的前缀。后文我们只考虑这种方便处理的编码。  
为了便于理解下面举出一些例子。

记 $X$ 为 $\vec V$ 的某维。$X$ 有 $4$ 种取值 $0,1,2,3$。  
我们可以采取 $0\to00,1\to01,2\to10,3\to11$ 这种映射方式。这是方便处理的，因为不存在一个取值编码为另一个取值编码的前缀。我们记这种编码方法为 $\text A$。  
有很多种方便处理的编码，$0\to0,1\to10,2\to110,3\to111$ 也是一种方便处理的编码。我们记这种编码方法为 $\text B$。  
$0\to0,1\to1,2\to00,3\to01$ 是不方便处理的编码，因为 $0$ 是 $00$ 的前缀，$0$ 是 $01$ 的前缀。

方便处理的编码构成合法比特序列到若干维随机向量的双射，这个太显然了我就不证明了。  
为了起到节约资源的效果，我们要使期望总码长最短。由瓦尔德等式，总码长期望是停时期望乘每维期望码长。所以我们只要考虑某一维上的取值就行了。

记 $X$ 为 $\vec V$ 的某维。$\mathbb P(X=0)=\frac12,\mathbb P(X=1)=\frac14,\mathbb P(X=2)=\mathbb P(X=3)=\frac18$。  
对于上文的编码方式 $\text A$，其期望码长为 $\frac12\times2+\frac14\times2+\frac18\times2+\frac18\times2=2$。  
对于上文的编码方式 $\text B$，其期望码长为 $\frac12\times1+\frac14\times2+\frac18\times3+\frac18\times3=\frac74$。  
所以，在 $X$ 的分布列为以上情况时，编码 $\text B$ 优于编码 $\text A$。

---

证明：$X$ 的可能取值为 $x_1,x_2,\cdots,x_n$，为了把他编码为长度 $b_1,b_2,\cdots,b_n$ 的编码，其充要条件为

$$
\sum_{i=1}^n2^{-b_i}\le1
$$


记 $w_j=\sum\limits_{i=1}^n[j=b_i]$。  
显然 $w_1\le2$。长度为 $j$ 的编码有 $2^j$ 种，但是有 $w_{j-1}$ 种不能使用，因为会有相同的前缀。所以 $w_j\le2^j-2w_{j-1}$。  
根据这个不等递推，那么对于任意 $T$ 均有

$$
\begin{aligned}
\sum_{j=1}^Tw_j2^{T-j}&\le2^T\\
\sum_{j=1}^Tw_j2^{-j}&\le1\\
\sum_{j=1}^\infty w_j2^{-j}&\le1\\
\sum_{i=1}^n2^{-b_i}&\le1
\end{aligned}
$$

<p align="right" style="font-size:1.5rem;">■</p>

---

无噪声编码定理：随机变量 $X\in\lbrace x_1,x_2,\cdots,x_n\rbrace$，其中 $\mathbb P(X=x_i)=p_i$。设有一个方便处理的编码方式，编码后长度为 $b_1,b_2,\cdots,b_n$，记 $Y$ 为 $X$ 编码后的期望码长，那么

$$
\mathbb E[Y]=\sum_{i=1}^np_ib_i\ge\mathbb H[X]=-\sum_{i=1}^np_i\log p_i
$$

记

$$
q_i=\frac{2^{-b_i}}{\sum_{j=1}^n2^{-b_j}}
$$

那么

$$
\begin{aligned}
-\sum_{i=1}^np_i\log\frac{p_i}{q_i}&=-\log\mathrm e\sum_{i=1}^np_i\ln\frac{p_i}{q_i}\\
&=\log\mathrm e\sum_{i=1}^np_i\ln\frac{q_i}{p_i}\\
&\le\log\mathrm e\sum_{i=1}^np_i(\frac{q_i}{p_i}-1)\\
&\le\log\mathrm e\sum_{i=1}^n(q_i-p_i)\\
&\le\log\mathrm e\sum_{i=1}^nq_i-\log\mathrm e\sum_{i=1}^np_i\\
&=0
\end{aligned}
$$

由此

$$
\begin{aligned}
\mathbb H[X]&=-\sum_{i=1}^np_i\log p_i\\
&\le-\sum_{i=1}^np_i\log q_i\\
&=\sum_{i=1}^np_ib_i+\log\sum_{i=1}^n2^{-b_i}\\
&\le\sum_{i=1}^np_ib_i=\mathbb E[Y]
\end{aligned}
$$

最后去掉 $\log\sum\limits_{i=1}^n2^{-b_i}$ 的原因是因为这是一个方便处理的编码方式，所以 $\sum\limits_{i=1}^n2^{-b_i}\le1$。
<p align="right" style="font-size:1.5rem;">■</p>

---

对于大部分随机向量不存在编码方式使得 $\mathbb E[Y]=\mathbb H[X]$。但是总存在编码方式编码方式使得与 $\mathbb H[X]$ 的差 $<1$。  
记 $n_i=\lceil-\log p_i\rceil$，那么 $\sum\limits_{i=1}^n2^{-n_i}\le\sum\limits_{i=1}^n2^{\log p_i}=\sum\limits_{i=1}^np_i=1$。  
注意，$\sum\limits_{i=1}^n2^{-b_i}\le1$ 和方便编码是充要条件，所以取 $b_i=n_i$，所以这是个方便处理的编码。  
由于 $-\log p_i\le n_i\le-\log p_i+1$，

$$
\mathbb E[Y]=\sum_{i=1}^nn_ip_i,\\
-\sum_{i=1}^np_i\log p_i\le\mathbb E[Y]<-\sum_{i=1}^np_i\log p_i+1\\
\mathbb H[X]\le\mathbb E[Y]<\mathbb H[X]+1
$$

哈夫曼编码的方式：

- 初始有 $n$ 个以 $p_i$ 作为根节点权值，只有根节点的二叉树，得到一个二叉树森林 $F$。
- 从 $F$ 中选取根节点权值最小的两颗二叉树，分别作为左子树和右子树建立一颗新的二叉树，这个二叉树根节点的权值是其左右子树根节点权值之和。
- 从 $F$ 中删除作为左、右子树的两棵二叉树，并将新建立的二叉树加入到 $F$ 中。
- 重复 2、3 步，当 $F$ 中只剩下一棵二叉树时，这棵二叉树就是哈夫曼树。
- 以 $x_1,x_2,\cdots,x_n$ 作为叶节点，$p_i$ 作为权值构造哈夫曼树。规定哈夫曼编码树的左分支代表 $0$，右分支代表 $1$，则从根结点到每个叶结点所经过的路径组成的 $0,1$ 序列即为该叶结点对应字符的编码。

实际上，当采取哈夫曼编码时，$\mathbb E[Y]$ 最小，运用调整法可证。

### 香农定理

在实际生活中，发送编码会受到干扰。比如发送了 $111011$，却接收到了 $011011$，这会产生解码错误。  
如果我们从位置 $\text A$ 发送一段比特序列到位置 $\text B$，每位出错（即 $0$ 变成 $1$，$1$ 变成 $0$）的概率为 $p$，每位出错是独立的，那么这就是一个二进制对称通道。  
一种避免出错的方法就是把比特序列重复发 $3$ 次，出现冲突就取多数。  
当 $p=0.2$ 时，出错的概率就降到 $0.2^3+\binom310.2^2\times0.8=0.104$。  
虽然这种重复编码的方式能够降低出错率，但是牺牲了编码效率。但是，存在一种编码方式，能够有足够大的概率获得正确的结果。  
一个 $(c_1,c_2)$ 编码函数 $\operatorname{Enc}$：$[0,1]^{c_1}\to[0,1]^{c_2}$ 以长度为 $c_1$ 的比特序列作为输入，长度为 $c_2$ 的比特序列作为输出。  
一个 $(c_1,c_2)$ 解码函数 $\operatorname{Dec}$：$[0,1]^{c_2}\to[0,1]^{c_1}$ 以长度为 $c_2$ 的比特序列作为输入，长度为 $c_1$ 的比特序列作为输出。  
编码函数把长度为 $c_1$ 的比特序列转为长度为 $c_2$ 的比特序列，通过通道发送过去，解码函数把长度为 $c_2$ 的比特序列转为长度为 $c_1$ 的比特序列。

香农定理：对于一个 $p<\frac12$ 的二进制对称通道以及任意常数 $\delta,\gamma>0$，当 $n$ 足够大时：

- 对任意 $k\le n(1-\mathbb H(p)-\delta)$，存在 $(k,n)$ 编码函数和解码函数，使得不能得到正确信息的概率至多为 $\gamma$。
- 对任意 $k\ge n(1-\mathbb H(p)+\delta)$，不存在 $(k,n)$ 编码函数和解码函数，使得得到正确信息的概率至少为 $\gamma$。

证明有点太复杂了，咕咕咕……等我有一天想补了就补上。好在香农帮我们证明过了。  
香农定理证明了足够长的传输任意接近二进制对称通道的代码的存在性。  
香农证明了这个定理之后并没有给出具体的代码，所以又过了几十年才找到了几乎最优的实际代码。