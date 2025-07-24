---
layout: post
title: "整体二分的不带修写法"
tags: 笔记
---

对于每个询问都可以二分的题目，可以将所有询问放在 `vector` 中。假设当前二分的答案区间为 $[l,r]$，按照比较结果把询问分成答案在左边和答案在右边，递归处理答案在左边 $[l,mid]$ 和答案在右边 $[mid+1,r]$。  
但是每次都进行 check 时，需要把 $[l,r]$ 这一段的所有操作拿出来，太慢了。不妨使用类似莫队的方法，使用一个指针来辅助快速 check。

P3527 [POI 2011] MET-Meteors
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
int n,m,k,p[N],ans[N],a[N],b[N],c[N];
vector<int>g[N];
struct{
	lolu d[N];
	void add(int x,int y){
		for(;x<=m;x+=x&-x)
			d[x]+=y;
	}
	lolu ask(int x){
		lolu y=0;
		for(;x;x-=x&-x)
			y+=d[x];
		return y;
	}
}tr;
#define mid ((l+r)>>1)
void solve(int l,int r,vector<int>&q){
	static int D=0;
	if(l==r){for(int i:q)ans[i]=l;return;}
	auto upd=[](int x,int z){
		int tmp=c[x]*z;
		if(a[x]<=b[x]){
			tr.add(a[x],tmp);
			if(b[x]<=m)tr.add(b[x]+1,-tmp);
		}else{
			tr.add(1,tmp);
			if(b[x]<=m)tr.add(b[x]+1,-tmp);
			tr.add(a[x],tmp);
		}
	};
	while(D<mid)upd(++D,1);
	while(D>mid)upd(D--,-1);
	vector<int>q1,q2;
	for(int i:q){
		lolu sum=0;
		for(int j:g[i])sum+=tr.ask(j);
		(sum>=p[i]?q1:q2).push_back(i);
	}
	solve(l,mid,q1);solve(mid+1,r,q2);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>m;
	for(int i=1;i<=m;i++){
		int o;cin>>o;
		g[o].push_back(i);
	}
	for(int i=1;i<=n;i++)cin>>p[i];
	cin>>k;
	for(int i=1;i<=k;i++)cin>>a[i]>>b[i]>>c[i];
	vector<int>tmp;tmp.resize(n);for(int i=0;i<n;i++)tmp[i]=i+1;
	solve(1,k+1,tmp);
	for(int i=1;i<=n;i++)
		if(ans[i]<=k)cout<<ans[i]<<'\n';
		else cout<<"NIE\n";
	return 0;
}
```

P3834 【模板】可持久化线段树 2
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
using tiiii=tuple<int,int,int,int>;
mt19937_64 rng(random_device{}());
constexpr int N=2e5+7;
int n,m,a[N],ans[N];
basic_string<int>b,p[N];
struct{
	int d[N];
	void add(int x,int y){
		for(;x<=n;x+=x&-x)
			d[x]+=y;
	}
	int ask(int x){
		int y=0;
		for(;x;x-=x&-x)
			y+=d[x];
		return y;
	}
}tr;
vector<tiiii>Q;
#define mid ((l+r)>>1)
void solve(int l,int r,vector<tiiii>&q){
	static int D=-1;
	if(l==r){for(auto[x,y,k,id]:q)ans[id]=b[l];return;}
	auto upd=[](int x,int z){for(int y:p[x])tr.add(y,z);};
	while(D<mid)upd(++D,1);
	while(D>mid)upd(D--,-1);
	vector<tiiii>q1,q2;
	for(auto[x,y,k,id]:q)
		(tr.ask(y)-tr.ask(x-1)>=k?q1:q2).emplace_back(x,y,k,id);
	solve(l,mid,q1);solve(mid+1,r,q2);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>m;
	for(int i=1;i<=n;i++)cin>>a[i],b+=a[i];
	sort(all(b));b.erase(unique(all(b)),b.end());
	for(int i=1;i<=n;i++)p[lower_bound(all(b),a[i])-b.begin()]+=i;
	for(int i=1,x,y,k;i<=m;i++)cin>>x>>y>>k,Q.emplace_back(x,y,k,i);
	solve(0,siz(b)-1,Q);
	for(int i=1;i<=m;i++)cout<<ans[i]<<'\n';
	return 0;
}
```