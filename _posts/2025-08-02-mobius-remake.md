---
layout: post
title: "莫比乌斯函数重置版"
tags: 笔记 数学
---

$$
\mu(n)=\left\{
\begin{matrix}
1&n=1\\
0&n 含有非平凡平方因子\\
(-1)^k&其中 k 为 n 本质不同的质因子个数
\end{matrix}
\right.
$$

<!-- 这个答辩似乎看不懂……不如换个形式去描述一下。   -->
换句话说，我们定义 $\mu(1)=1$。  
使用唯一分解定理把 $n$ 写为 $\prod_{i=1}^k{p_i}^{c_i}$，如果 $\max_{c_k}>1$ 那么 $\mu(n)=0$。  
否则 $\mu(n)=(-1)^k$。  

---
由于莫比乌斯也是高贵的积性函数，可以线性筛预处理：
```cpp
mu[1]=1;
for(int i=2;i<N;i++){
	if(!pr[i])pt+=i,mu[i]=-1;
	for(int j:pt){
		if(i*j>=N)break;
		pr[i*j]=true;
		if(i%j==0)break;
		mu[i*j]=-mu[i];
	}
}
```

莫比乌斯函数从何而来？得从反演的角度来考虑。

如果有

$$
f(n)=\sum_{d\mid n}g(d)
$$

那么

$$
g(n)=\sum_{d\mid n}\mu(d)f(\frac nd)
$$

系数 $\mu$ 就是莫比乌斯函数。

---

$$
\sum_{d\mid n}\mu(d)=\varepsilon(n)=[n=1]=\left\{
\begin{matrix}
1&n=1\\
0&n\ne1
\end{matrix}
\right.
$$

证明。把 $n$ 写为 $\prod_{i=1}^k{p_i}^{c_i}$，那就是这些质因子自由组合弄出的倍数也就是 $\prod_{i=1}^k{p_i}^{d_i},d_i\in[0,c_i]$。  
如果对于某个数 $x$，存在 $d_i>1$，那么这个数的莫比乌斯函数必然为 $0$ 无需考虑。否则 $d_i\le1$，相当于每个因子都可以选或不选，选了 $i$ 个因子时 $\mu(x)=(-1)^i$，因此

$$
\sum_{i=0}^k(-1)^i\binom ki=(1-1)^k=0
$$

当 $n=1$ 时是例外，此时 $\sum\limits_{d\mid1}\mu(d)=1$。  

---

如果我们设个函数 $1(n)=1$，那么

$$
\varepsilon(n)=\sum_{d\mid n}\mu(d)=\sum_{d\mid n}\mu(d)1(\frac nd)
$$

这是莫比乌斯反演后的形式，不妨反演回去，那么

$$
1(n)=\sum_{d\mid n}\varepsilon(d)
$$

这个式子显然成立，如果我们通过该式去莫比乌斯反演，同样可以推出

$$
\sum_{d\mid n}\mu(d)=\varepsilon(n)
$$

---

不妨引入狄利克雷卷积来简化描述。  
对于数论函数 $f,g$，定义其狄利克雷卷积 $f*g$ 为

$$
(f*g)(n)=\sum_{d\mid n}f(d)g(\frac nd)
$$

显然狄利克雷卷积满足交换律和结合律。

常见数论函数
- $1(n)=1$
- $i(n)=n$
- $\varepsilon(n)=[n=1]$
- $\varphi(n)$，即欧拉函数
- $\mu(n)$，即莫比乌斯函数

莫比乌斯反演的本质就是在狄利克雷卷积中，$1,\mu$ 互为逆元。  
也就是说 $f=g*1\Longleftrightarrow g=\mu*f$。

我们知道 $i=\varphi*1$，因此 $\varphi=\mu*i$。  
我们知道 $1=\varepsilon*1$，因此 $\varepsilon=\mu*1$

---

对于大部分的莫比乌斯反演题来说，都是去利用

$$
\sum_{d\mid n}\mu(d)=[n=1]
$$

就像单位根反演解决的是 $[n\bmod 5]$，莫比乌斯反演解决的是 $[n=1]$。

比如带入 $n=\gcd(a,b)$，那么

$$
\sum_{d\mid\gcd(a,b)}\mu(d)=[\gcd(a,b)=1]
$$


---

[P2522 [HAOI2011] Problem b](https://www.luogu.com.cn/problem/P2522)

二维前缀和转化后的题意：

$$
\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=k]
$$

注意到 $i,j$ 必须恰好都是 $k$ 的倍数，不妨做变量代换 $n\gets\lfloor\frac nk\rfloor,m\gets\lfloor\frac mk\rfloor$，那么只需求

$$
\begin{aligned}
\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=1]
&=\sum_{i=1}^n\sum_{j=1}^m\sum_{d\mid\gcd(i,j)}\mu(d)\\
&=\sum_d\mu(d)\left\lfloor\frac nd\right\rfloor\left\lfloor\frac md\right\rfloor
\end{aligned}
$$

二维整除分块即可。

---
[P2257 YY的GCD](https://www.luogu.com.cn/problem/P2257)

$$
\sum_{t\in\mathbb P}\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=t]
$$

直接进行刚刚相同的转化

$$
\begin{aligned}
\sum_{t\in\mathbb P}\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=t]&=\sum_{t\in\mathbb P}\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}[\gcd(i,j)=1]\\
&=\sum_{t\in\mathbb P}\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}\sum_{d\mid\gcd(i,j)}\mu(d)\\
&=\sum_{t\in\mathbb P}\sum_d\mu(d)\left\lfloor\frac n{td}\right\rfloor\left\lfloor\frac m{td}\right\rfloor
\end{aligned}
$$

令 $f(t)=[t\in\mathbb P],h=f*\mu$，那么原式就是

$$
\sum_{t\in\mathbb P}\sum_d\mu(d)\left\lfloor\frac n{td}\right\rfloor\left\lfloor\frac m{td}\right\rfloor=\sum_wh(w)\left\lfloor\frac n{w}\right\rfloor\left\lfloor\frac m{w}\right\rfloor
$$

---

来看直接求 $\gcd$ 和的情况。
$$
\begin{aligned}
\sum_{i=1}^n\sum_{j=1}^m\gcd(i,j)&=\sum_tt\sum_{i=1}^n\sum_{j=1}^m[\gcd(i,j)=t]\\
&=\sum_tt\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}[\gcd(i,j)=1]\\
&=\sum_tt\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}\sum_{d\mid\gcd(i,j)}\mu(d)\\
&=\sum_tt\sum_d\mu(d)\left\lfloor\frac n{td}\right\rfloor\left\lfloor\frac m{td}\right\rfloor
\end{aligned}
$$

$i*\mu=\varphi$，那么原式就是

$$
\sum_tt\sum_d\mu(d)\left\lfloor\frac n{td}\right\rfloor\left\lfloor\frac m{td}\right\rfloor=\sum_w\varphi(w)\left\lfloor\frac n{w}\right\rfloor\left\lfloor\frac m{w}\right\rfloor
$$

---

[P1829 [国家集训队] Crash的数字表格 / JZPTAB](https://www.luogu.com.cn/problem/P1829)

来看直接求 $\operatorname{lcm}$ 和的情况。
$$
\begin{aligned}
\sum_{i=1}^n\sum_{j=1}^m\operatorname{lcm}(i,j)&=\sum_{i=1}^n\sum_{j=1}^m\frac{ij}{\gcd(i,j)}\\
&=\sum_t\sum_{i=1}^n\sum_{j=1}^m\frac{ij}t[\gcd(i,j)=t]\\
&=\sum_tt\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}ij[\gcd(i,j)=1]\\
&=\sum_tt\sum_{i=1}^{\lfloor\frac nt\rfloor}\sum_{j=1}^{\lfloor\frac mt\rfloor}ij\sum_{d\mid\gcd(i,j)}\mu(d)\\
&=\sum_tt\sum_dd^2\mu(d)\sum_{i=1}^{\lfloor\frac n{td}\rfloor}i\sum_{j=1}^{\lfloor\frac m{td}\rfloor}j\\
\end{aligned}
$$

令 $g(d)=d^2\mu(d),h=i*g,s(n)=\frac{n(n+1)}2$，那么原式就是

$$
\sum_tt\sum_dd^2\mu(d)\sum_{i=1}^{\lfloor\frac n{td}\rfloor}i\sum_{j=1}^{\lfloor\frac m{td}\rfloor}j=\sum_wh(w)s\left(\left\lfloor\frac nw\right\rfloor\right)s\left(\left\lfloor\frac mw\right\rfloor\right)
$$

---

https://codeforces.com/group/MIyYz3rj9b/contest/621587/problem/C

给定 $n$ 个数 $a_i(a_i\le3\times10^5)$，对于每个数 $a_i$ 求出 $n$ 个数中与 $a_i$ 互质的最大的数。  
保证所有数中有个 $1$，因此不存在没有数与 $a_i$ 互质的情况。

对于其中的某个数 $a_x$，我们不妨考虑使用二分去寻找其答案。  
先将所有数按照降序排序。不妨假设我们已经确定了 $a_x$ 的答案在区间 $[l,r]$ 中（$l,r$ 是下标），那么如果

$$
\sum_{i\in[l,mid]}[\gcd(a_i,a_x)=1]>0
$$

那就说明答案在 $[l,mid]$，否则答案就在 $[mid+1,r]$。

$$
\begin{aligned}
\sum_{i\in[l,mid]}[\gcd(a_i,a_x)=1]&=\sum_{i\in[l,mid]}\sum_{d\mid\gcd(a_i,a_x)}\mu(d)\\
&=\sum_{d\mid a_x}\mu(d)\sum_{i\in[l,mid]}[a_i\bmod d=0]
\end{aligned}
$$

相当于我们只需要对于每个 $d$ 求出区间 $[l,mid]$ 有多少为其倍数即可。  
复杂度二分一个 $\log$，枚举 $a_x$ 因子复杂度为 $\mathrm d(n)$。对于单个数，可以前缀和预处理 $[a_i\bmod d=0]$，总复杂度为 $\mathcal O(n\mathrm d(n)\log n+n\mathrm d(n))=\mathcal O(n\mathrm d(n)\log n)$。  
对于所有数，其实只要整体二分就好了。处理 $[a_i\bmod d=0]$ 只需要在指针移动时进行处理即可。  
但是本体有点卡常，有两个小优化：
- 对读入的所有数去重再整体二分；
- 对莫比乌斯函数值为 $0$ 的因子无需处理。

```cpp
#include<bits/stdc++.h>
#define siz(x) int((x).size())
#define all(x) std::begin(x),std::end(x)
#define fi first
#define se second
using namespace std;
using unt=unsigned;
using loli=long long;
using lolu=unsigned long long;
using pii=pair<int,int>;
mt19937_64 rng(random_device{}());
constexpr int N=3e5+7;
int n,a[N],ans[N],cnt[N];
int pr[N],mu[N];
basic_string<int>pt,b[N],qc;
#define mid ((l+r)>>1)
void solve(int l,int r,vector<int>&q){
	if(q.empty())return;
	static int D=-1;
	if(l==r){for(int i:q)ans[qc[i]]=qc[l];return;}
	auto upd=[](int x,int z){
		for(int y:b[qc[x]])
			cnt[y]+=z;
	};
	while(D<mid)upd(++D,1);
	while(D>mid)upd(D--,-1);
	vector<int>q1,q2;
	for(int i:q){
		int sum=0;
		for(int y:b[qc[i]])
			sum+=cnt[y]*mu[y];
		(sum?q1:q2).push_back(i);
	}
	solve(l,mid,q1);solve(mid+1,r,q2);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	mu[1]=1;
	for(int i=2;i<N;i++){
		if(!pr[i])pt+=i,mu[i]=-1;
		for(int j:pt){
			if(i*j>=N)break;
			pr[i*j]=true;
			if(i%j==0)break;
			mu[i*j]=-mu[i];
		}
	}
	for(int i=1;i<N;i++)if(mu[i])
		for(int j=i;j<N;j+=i)b[j]+=i;
	cin>>n;
	for(int i=1;i<=n;i++)
		cin>>a[i],qc+=a[i];
	sort(all(qc),greater<>());
	qc.erase(unique(all(qc)),qc.end());
	vector<int>tmp(n);
	for(int i=0;i<siz(qc);i++)tmp[i]=i;
	solve(0,siz(qc)-1,tmp);
	for(int i=1;i<=n;i++)cout<<ans[a[i]]<<' ';
	return 0;
}
```
---
[P5518 [MtOI2019] 幽灵乐团](https://www.luogu.com.cn/problem/P5518)第一部分分

$$
\begin{aligned}
\prod_{i=1}^A\prod_{i=1}^B\prod_{i=1}^C\frac{\operatorname{lcm}(i,j)}{\gcd(i,k)}&=\prod_{i=1}^A\prod_{i=1}^B\prod_{i=1}^C\frac{ij}{\gcd(i,j)\gcd(i,k)}\\
&=\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^Cij\times\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^C\frac1{\gcd(i,j)}\times\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^C\frac1{\gcd(i,k)}\\
&=\left(\prod_{i=1}^A\prod_{j=1}^Bij\right)^C\times\left(\prod_{i=1}^A\prod_{j=1}^B\frac1{\gcd(i,j)}\right)^C\times\left(\prod_{i=1}^A\prod_{k=1}^C\frac1{\gcd(i,k)}\right)^B\\
&=\left(A!B!\right)^C\times\left(\prod_{i=1}^A\prod_{j=1}^B\frac1{\gcd(i,j)}\right)^C\times\left(\prod_{i=1}^A\prod_{k=1}^C\frac1{\gcd(i,k)}\right)^B\\
\end{aligned}
$$

因此只需求

$$
\begin{aligned}
\prod_{i=1}^A\prod_{j=1}^B\frac1{\gcd(i,j)}&=\prod_t\prod_{i=1}^{\lfloor\frac At\rfloor}\prod_{j=1}^{\lfloor\frac Bt\rfloor}\left(\frac1t\right)^{[\gcd(i,j)=1]}\\
&=\prod_t\prod_{i=1}^{\lfloor\frac At\rfloor}\prod_{j=1}^{\lfloor\frac Bt\rfloor}\left(\frac1t\right)^{\sum\limits_{d\mid\gcd(i,j)}\mu(d)}\\
&=\prod_t\prod_d\prod_{i=1}^{\lfloor\frac A{td}\rfloor}\prod_{j=1}^{\lfloor\frac B{td}\rfloor}\left(\frac1t\right)^{\mu(d)}\\
&=\prod_t\prod_d\left(\frac1t\right)^{\mu(d)\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}\\
\end{aligned}
$$

令

$$
h(n)=\prod_{d\mid n}\left(\frac dn\right)^{\mu(d)}
$$

那么原式就是

$$
\prod_t\prod_d\left(\frac1t\right)^{\mu(d)\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}=\prod_wh^{\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}(w)
$$
---

[P5518 [MtOI2019] 幽灵乐团](https://www.luogu.com.cn/problem/P5518)第二部分分

令 $s(n)=\frac{n(n+1)}2$

$$
\begin{aligned}
\prod_{i=1}^A\prod_{i=1}^B\prod_{i=1}^C\left(\frac{\operatorname{lcm}(i,j)}{\gcd(i,k)}\right)^{ijk}&=\left(\prod_{i=1}^A\prod_{i=1}^B\prod_{i=1}^C\frac{ij}{\gcd(i,j)\gcd(i,k)}\right)^{ijk}\\
&=\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^C{ij}^{ijk}\times\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^C\left(\frac1{\gcd(i,j)}\right)^{ijk}\times\left(\prod_{i=1}^A\prod_{j=1}^B\prod_{k=1}^C\frac1{\gcd(i,k)}\right)^{ijk}\\
&=\left(\prod_{i=1}^A\prod_{j=1}^B{ij}^{ij}\right)^{s(C)}\times\left(\left(\prod_{i=1}^A\prod_{j=1}^B\frac1{\gcd(i,j)}\right)^{ij}\right)^{s(C)}\times\left(\left(\prod_{i=1}^A\prod_{k=1}^C\frac1{\gcd(i,k)}\right)^{ik}\right)^{s(B)}\\
% &=\left(A!B!\right)^{s(C)}\times\left(\prod_{i=1}^A\prod_{j=1}^B\frac1{\gcd(i,j)}\right)^{s(C)}\times\left(\prod_{i=1}^A\prod_{k=1}^C\frac1{\gcd(i,k)}\right)^{s(C)}\\
\end{aligned}
$$

因此只需求

$$
\begin{aligned}
\prod_{i=1}^A\prod_{j=1}^B\left(\frac1{\gcd(i,j)}\right)^{ij}&=\prod_t\prod_{i=1}^{\lfloor\frac At\rfloor}\prod_{j=1}^{\lfloor\frac Bt\rfloor}\left(\frac1t\right)^{ij[\gcd(i,j)=1]}\\
&=\prod_t\prod_{i=1}^{\lfloor\frac At\rfloor}\prod_{j=1}^{\lfloor\frac Bt\rfloor}\left(\frac1t\right)^{ijt^2\sum\limits_{d\mid\gcd(i,j)}\mu(d)}\\
&=\prod_t\prod_d\prod_{i=1}^{\lfloor\frac A{td}\rfloor}\prod_{j=1}^{\lfloor\frac B{td}\rfloor}\left(\frac1t\right)^{ijt^2d^2\mu(d)}\\
&=\prod_t\prod_d\left(\frac1t\right)^{t^2d^2\mu(d)s(A)s(B)\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}\\
\end{aligned}
$$

令

$$
h(n)=\prod_{d\mid n}\left(\frac dn\right)^{(\frac dn)^2d^2\mu(d)}
$$

那么原式就是

$$
\prod_t\prod_d\left(\frac1t\right)^{\mu(d)\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}=\prod_wh^{s(A)s(B)\lfloor\frac A{td}\rfloor\lfloor\frac B{td}\rfloor}(w)
$$