---
layout: post
title: "FWT 的矩阵理解"
tags: 笔记 算法
---

在学习 FFT 的时候，我们对序列 $A,B$ 做了一次 $\mathrm{dft}$ 变换，将函数值转化为了点值，使得 $\mathrm{dft}A_i\times\mathrm{dft}B_i=\mathrm{dft}C_i$，这样我们再对点值 $\mathrm{dft}C_i$ 做一次 $\mathrm{dft^{-1}}$ 变换，就将点值还原成了序列。

现在，我们来扩展一下 $\mathrm{dft}$ 的定义，我们无需关心 $\mathrm{dft}$ 是不是什么点值，只需让其满足性质 $\mathrm{dft}A_i\times\mathrm{dft}B_i=\mathrm{dft}C_i$，并且存在 $\mathrm{dft}$ 的逆变换 $\mathrm{dft^{-1}}$，那么我们就认为这是一个广义的 $\mathrm{dft}$。

我们现在用这种变换来解决 $\text{and}$ 卷积，$\text{or}$ 卷积，$\text{xor}$ 卷积等位运算卷积。

$\text{and}$ 卷积 $C=A\wedge B$ 的定义：
$$
C_k=\sum_{i\wedge j=k}A_iB_j
$$

$\text{or}$ 卷积 $C=A\vee B$ 的定义：
$$
C_k=\sum_{i\vee j=k}A_iB_j
$$

$\text{xor}$ 卷积 $C=A\oplus B$ 的定义：
$$
C_k=\sum_{i\oplus j=k}A_iB_j
$$

不妨认为位运算上的 $\mathrm{dft}$ 是线性变换，称其为 $\mathrm{fwt}$，也就是说

$$
A\times f=\mathrm{fwt}A
$$

$f$ 是一个 $2^n\times 2^n$ 的矩阵，也就是说

$$
\sum_{j=0}^{2^n-1}A_jf_{j,i}=\mathrm{fwt}A_i
$$

根据定义，$\mathrm{dft}A_i\times\mathrm{dft}B_i=\mathrm{dft}C_i$，因此 $f_{j,i}f_{k,i}=f_{j\odot k,i}$，其中 $\odot$ 是位运算卷积对应的位运算。

坑蒙拐骗一下，假如 $n=1$，这个时候 $A$ 只有两个元素 $A_0=a,A_1=b$，$B$ 只有两个元素 $B_0=c,B_1=d$，如果 $C=A\wedge B$，那么 $C_0=ac,C_1=ad+bc+bd$。  
可以证明的是，整个卷积过程可以看作每维独立的卷积，即

```cpp
for(int i=0;i<n;i++)
	for(int j=0;j<(1<<n);j++)
if(j>>i&1)
{
	// a[j^(1<<i)] 对应 A[0]
	// a[j] 对应 A[1]
}
```

这样，$f$ 实际上只是一个 $2\times 2$ 的矩阵，我们不妨设

$$
f=\begin{bmatrix}
w&x\\
y&z
\end{bmatrix}
$$

那么

$$
\mathrm{fwt}A=A\times f=\begin{bmatrix}a&b\end{bmatrix}\times\begin{bmatrix}w&x\\y&z\end{bmatrix}=\begin{bmatrix}aw+by&ax+bz\end{bmatrix}\\
\mathrm{fwt}B=B\times f=\begin{bmatrix}c&d\end{bmatrix}\times\begin{bmatrix}w&x\\y&z\end{bmatrix}=\begin{bmatrix}cw+dy&cx+dz\end{bmatrix}\\
$$

根据定义，$\mathrm{fwt}A_i\times\mathrm{fwt}B_i=\mathrm{fwt}C_i$

$$
\mathrm{fwt}C=\begin{bmatrix}(aw+by)(cw+dy)&(ax+bz)(cx+dz)\end{bmatrix}
$$

如果此时是 $\text{or}$ 卷积，那么

$$
C=\begin{bmatrix}ac&ad+bc+bd\end{bmatrix}\\
\begin{aligned}
\mathrm{fwt}C&=C\times f=\begin{bmatrix}ac&ad+bc+bd\end{bmatrix}\times\begin{bmatrix}w&x\\y&z\end{bmatrix}
\\
&=\begin{bmatrix}acw+(bc+ad+bd)y&acx+(bc+ad+bd)z\end{bmatrix}
\end{aligned}
$$

对比两种方法算出来的 $\mathrm{fwt}C$ 的系数，可以解出

$$
\left\{
\begin{matrix}
w=w^2\\
y=wy=y^2\\
x=x^2\\
z=xz=z^2\\
wz-xy\ne0
\end{matrix}
\right.
$$

最后一个限制是因为得满足矩阵 $f$ 有逆，其行列式不为 $0$。

有两组解：

$$
f=\begin{bmatrix}1&1\\0&1\end{bmatrix}或\begin{bmatrix}1&1\\1&0\end{bmatrix}
$$

实际上两组解均可以，这里我们用第一种，那么

$$
\mathrm{fwt}A=A\times f=\begin{bmatrix}a&b\end{bmatrix}\times\begin{bmatrix}1&1\\0&1\end{bmatrix}=\begin{bmatrix}a&a+b\end{bmatrix}\\
$$

其对应的代码就是

```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)a[j]+=a[j^(1<<i)];
```

对于第一组解

$$
f^{-1}=\begin{bmatrix}1&-1\\0&1\end{bmatrix}
$$

那么

$$
C=\mathrm{fwt}C\times f=\begin{bmatrix}p&q\end{bmatrix}\times\begin{bmatrix}1&-1\\0&1\end{bmatrix}=\begin{bmatrix}p&-p+q\end{bmatrix}\\
$$

其对应的代码就是

```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)c[j]-=c[j^(1<<i)];
```

全部代码：
```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)a[j]+=a[j^(1<<i)];
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)b[j]+=b[j^(1<<i)];
for(int j=0;j<(1<<n);j++)
	c[j]=a[j]*b[j];
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)c[j]-=c[j^(1<<i)];
for(int j=0;j<(1<<n);j++)
	cout<<c[j]<<' ';
```

$\text{and}$ 卷积类似 $\text{or}$ 卷积，不再赘述，仅给出 $f$，以及第一组解 $f$ 对应的代码。

$$
f=\begin{bmatrix}1&0\\1&1\end{bmatrix}或\begin{bmatrix}0&1\\1&1\end{bmatrix}
$$

```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)a[j^(1<<i)]+=a[j];
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)b[j^(1<<i)]+=b[j];
for(int j=0;j<(1<<n);j++)
	c[j]=a[j]*b[j];
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)c[j^(1<<i)]-=c[j];
for(int j=0;j<(1<<n);j++)
	cout<<c[j]<<' ';
```

对于 $\text{xor}$ 卷积，同理

$$
f=\begin{bmatrix}1&1\\-1&1\end{bmatrix}或\begin{bmatrix}1&1\\1&-1\end{bmatrix}
$$

仍然采用第一种，但是此时

$$
\mathrm{fwt}A=A\times f=\begin{bmatrix}a&b\end{bmatrix}\times\begin{bmatrix}1&1\\-1&1\end{bmatrix}=\begin{bmatrix}a-b&a+b\end{bmatrix}\\
$$

此时不是一句单纯的修改就能解决的，需要引入中间变量记录值。更好的代码实现方式是采用 `tie` 来绑定。

```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)tie(a[j^(1<<i)],a[j])=pair(a[j^(1<<i)]-a[j],a[j^(1<<i)]+a[j]);
```

而

$$
\mathrm{f^{-1}}=\begin{bmatrix}0.5&-0.5\\0.5&0.5\end{bmatrix}
$$

此时会涉及到除法，不可以直接除掉，应在模意义下乘以 $2$ 的乘法逆元。

```cpp
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)tie(a[j^(1<<i)],a[j])=pair(a[j^(1<<i)]-a[j],a[j^(1<<i)]+a[j]);
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)tie(b[j^(1<<i)],b[j])=pair(b[j^(1<<i)]-b[j],b[j^(1<<i)]+b[j]);
for(int j=0;j<(1<<n);j++)
	c[j]=a[j]*b[j];
for(int i=0;i<n;i++)for(int j=0;j<(1<<n);j++)
	if(j>>i&1)tie(c[j^(1<<i)],c[j])=pair((c[j^(1<<i)]+c[j])*ny,(-c[j^(1<<i)]+c[j])*ny);
for(int j=0;j<(1<<n);j++)
	cout<<c[j]<<' ';
```

对于子集卷积

$$
C_k=\sum_{i\vee j=k,i\wedge j=0}A_iA_j
$$

如果我们直接使用 $\text{or}$ 卷积，尽管能满足 $i\vee j=k$，但 $i\wedge j\ne0$ 的项也被算进去了。  
此时如果我们对 $2^n$ 个数按 $\text{pop}$ 分成 $n+1$ 组，其中第 $i$ 组的 $\text{pop}$ 均为 $i$，那么我们枚举 $A$ 中的 $\text{pop}$ 值 $c_1$，$B$ 中的 $\text{pop}$ 值 $c_2$，将他们的值仅转移到 $C$ 中的 $\text{pop}$ 值 $c_1+c_2$ 那组即可。

```cpp
for(int i=0;i<(1<<n);i++)
	cin>>a[pop(i)][i];
for(int i=0;i<(1<<n);i++)
	cin>>b[pop(i)][i];
for(int i=0;i<=n;i++){
	fwt_or(a[i]);
	fwt_or(b[i]);
}
for(int i=0;i<=n;i++)for(int j=0;j<=i;j++)
	for(int k=0;k<(1<<n);k++)
		c[i][k]+=a[j][k]*b[i-j][k];
for(int i=0;i<=n;i++){
	ifwt_or(c[i]);
}
for(int i=0;i<(1<<n);i++)
	cout<<c[pop(i)][i]<<' ';
```