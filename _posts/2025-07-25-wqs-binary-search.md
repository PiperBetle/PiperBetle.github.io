---
layout: post
title: "wqs 二分"
tags: 笔记 算法
---

应用场景：恰好选 $k$ 个，凹凸性。

$n$ 个物品，恰好选 $k$ 个/分成 $k$ 段，最大化收益。  
记 $c_{i,j}$ 表示将 $[1,i]$ 划分成 $j$ 总段的收益，凹凸性是指 $(j,c_{i,j})$ 形成一个凸包，即对于同一个 $i$，$c_{i,j+1}-c_{i,j}$ 具有单调性。

假设我们现在有个数字 $D$。由于 $(j,c_{i,j})$ 形成一个凸包，该凸包上至少有个点满足过这个点的斜率为 $D$ 的直线与该凸包相切。  

我们令 $f_i$ 是个 pair，其 `first`（y 坐标）记录了做完前 $i$ 个点产生的最大收益，其 `second`（x 坐标）记录了做完前 $i$ 个点产生最大收益时的最少段数。  

现在去二分 $D$，去考虑过哪个点做斜率为 $D$ 的直线与凸包相切。那么，相当于每个点的 `first` 都减去了若干个 $D$，并且若干个 $D$ 的 $D$ 的数量是关于 `second` 的一次函数。此时的最高点就是在原问题中，那个满足过该点斜率为 $D$ 的直线与该凸包相切的那个点减去距离原最高点的 `first` 乘以 $D$。

此时的最高点的 `second` 如果小于等于 $k$ 则可以更新答案，并且可以减小斜率去探测更大的 `first`；否则应增大斜率，减少切点的 `second` 去满足限制。

P1484 种树
```cpp
#include<bits/stdc++.h>
#define siz(x) int((x).size())
#define all(x) std::begin(x),std::end(x)
#define fi first
#define se second
#define int loli
using namespace std;
using unt=unsigned;
using loli=long long;
using lolu=unsigned long long;
using pii=pair<int,int>;
using pll=pair<loli,loli>;
mt19937_64 rng(random_device{}());
constexpr int N=3e5+7;
int n,m,a[N];
pll f[N][2];
loli ans;
pll solve(int D){
	f[0][0]=f[0][1]={0,0};
	auto wqs=[](const pll&x,const pll&y){
		if(x.fi>y.fi||(x.fi==y.fi&&x.se<y.se))return x;
		return y;
	};
	for(int i=1;i<=n;i++){
		f[i][0]=wqs(f[i-1][0],f[i-1][1]);
		f[i][1]={f[i-1][0].fi+a[i]+D,f[i-1][0].se+1};
	}
	return wqs(f[n][0],f[n][1]);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>m;
	for(int i=1;i<=n;i++)cin>>a[i];
	int l=-1e9,r=0;
	while(l<=r){
		int mid=((l+r)>>1);
		auto[y,x]=solve(mid);
		if(x<=m)ans=y-m*mid,l=mid+1;
		else r=mid-1;
	}
	cout<<ans;
	return 0;
}
```