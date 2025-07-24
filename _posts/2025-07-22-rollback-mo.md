---
layout: post
title: "回滚莫队速成"
tags: 笔记 算法
---

正常的莫队中，我们使用 $L,R$ 两个指针的移动来框出区间 $[l,r]$，可以发现这种移动是不满足可撤销性的。  
如果我们换一种指针的移动方式，使莫队具有可撤销性，那么配合可撤销数据结构就可以维护更多东西了。

不妨把所有左端点在同一块的询问放到一个 `vector` 中，然后将其按照右端点升序进行排序。  
如果左端点右端点在同一块，直接暴力做，做完全部撤销。  
否则，我们令右指针初始为当前块的右端点。对于每个询问，跟随右端点一直向右单调移动到 $r$，然后令莫队区间的左端点一直向左移动到 $l$，此时回答询问，然后撤销莫队区间的左端点的所有操作。  
具体写代码时可以并到一起。

有时写撤销操作比较麻烦，也可以直接记录原先状态，撤销时进行覆盖。会发现有的题目是加入简单，有的题目是撤销简单。如果是加入简单，不妨使用上述方法，然后将撤销变为原数据覆盖。

如果是撤销简单加入麻烦，先按照右端点降序进行排序。然后把这一块所有询问最左、右点中间的部分作为莫队区间。每次只需令右指针初始为所有询问最右点。对于每个询问，跟随右端点一直向左单调移动到 $r$，然后令莫队区间的左端点一直向右移动到 $l$，此时回答询问，然后撤销莫队区间的左端点的所有操作。  

P5906 【模板】回滚莫队&不删除莫队
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
using tiii=tuple<int,int,int>;
mt19937_64 rng(random_device{}());
constexpr int N=2e5+7,M=5e2+7;
int n,m,B,a[N],fl[M],fr[M],bel[N];
int pl[N],pr[N],tpl[N],tpr[N],ans[N];
vector<int>b;
vector<tiii>q[M];
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n;B=sqrt(n);
	for(int i=1;i<=n;i++){
		cin>>a[i];
		b.push_back(a[i]);
		bel[i]=bel[i-1]+(i%B==1);
	}
	sort(all(b));b.erase(unique(all(b)),b.end());
	for(int i=1;i<=n;i++){
		a[i]=lower_bound(all(b),a[i])-b.begin()+1;
		if(bel[i-1]!=bel[i])fl[bel[i]]=i;
		if(bel[i]!=bel[i+1])fr[bel[i]]=i;
	}
	cin>>m;
	for(int i=1;i<=m;i++){
		int l,r;cin>>l>>r;
		q[bel[l]].emplace_back(l,r,i);
	}
	auto add=[](int x,int&y){
		pl[a[x]]=min(pl[a[x]],x);
		pr[a[x]]=max(pr[a[x]],x);
		y=max(y,pr[a[x]]-pl[a[x]]);
	};
	for(int k=1;k<=bel[n];k++){
		memset(pl,0x3c,sizeof pl);
		memset(pr,0xc3,sizeof pr);
		sort(all(q[k]),[](const tiii&x,const tiii&y){
			return get<1>(x)<get<1>(y);
		});
		int D=fr[k],mx=0;
		for(auto[l,r,id]:q[k]){
			while(D<r)add(++D,mx);
			int tmp=mx;
			for(int i=min(r,fr[k]);i>=l;i--){
				tpl[a[i]]=pl[a[i]];
				tpr[a[i]]=pr[a[i]];
			}
			for(int i=min(r,fr[k]);i>=l;i--)
				add(i,tmp);
			for(int i=l;i<=min(r,fr[k]);i++){
				pl[a[i]]=tpl[a[i]];
				pr[a[i]]=tpr[a[i]];
			}
			ans[id]=tmp;
		}
	}
	for(int i=1;i<=m;i++)
		cout<<ans[i]<<'\n';
	return 0;
}
```

	
P8078 [WC2022] 秃子酋长
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
using tiii=tuple<int,int,int>;
mt19937_64 rng(random_device{}());
constexpr int N=5e5+7,M=757;
int n,m,B,a[N],fl[M],fr[M],bel[N];
int pos[N],pre[N],nxt[N];
loli sum,ans[N];
tiii qwq[N];
// bool vis[N];
bitset<N>vis;
vector<int>b;
vector<tiii>q[M];
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>m;
	B=1500;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		pos[a[i]]=i;
		bel[i]=bel[i-1]+(i%B==1);
	}
	for(int i=1;i<=n;i++){
		if(bel[i-1]!=bel[i])fl[bel[i]]=i;
		if(bel[i]!=bel[i+1])fr[bel[i]]=i;
	}
	for(int i=1;i<=m;i++){
		int l,r;cin>>l>>r;
		q[bel[l]].emplace_back(l,r,i);
	}
	for(int k=1;k<=bel[n];k++){
		if(q[k].empty())continue;
		sort(all(q[k]),[](const tiii&x,const tiii&y){
			return get<1>(x)>get<1>(y);
		});
		int D=get<1>(q[k].front());
		for(int i=fl[k];i<=D;i++)vis[a[i]]=true;
		b.clear();
		for(int i=1;i<=n;i++)if(vis[i])b.push_back(i);
		sum=0;
		for(int i=0;i<siz(b);i++){
			if(i)pre[b[i]]=b[i-1];else pre[b[i]]=0;
			if(i<siz(b)-1)nxt[b[i]]=b[i+1];else nxt[b[i]]=0;
			if(i)sum+=abs(pos[b[i]]-pos[b[i-1]]);
		}
		auto del=[](int x,loli&y){
			if(pre[x])y-=abs(pos[pre[x]]-pos[x]);
			if(nxt[x])y-=abs(pos[x]-pos[nxt[x]]);
			if(pre[x]&&nxt[x])y+=abs(pos[pre[x]]-pos[nxt[x]]);
			if(pre[x])nxt[pre[x]]=nxt[x];
			if(nxt[x])pre[nxt[x]]=pre[x];
		};
		for(auto[l,r,id]:q[k]){
			while(D>r)del(a[D--],sum);
			loli tmp=sum;
			for(int i=fl[k];i<l;i++){
				qwq[i]={pre[a[i]],a[i],nxt[a[i]]};
				del(a[i],tmp);
			}
			ans[id]=tmp;
			for(int i=l-1;i>=fl[k];i--){
				auto[x,y,z]=qwq[i];
				if(x)nxt[x]=y;
				if(z)pre[z]=y;
			}
		}
		for(int i=fl[k];i<=get<1>(q[k].front());i++)vis[a[i]]=false;
		for(int i:b)pre[i]=nxt[i]=0;
	}
	for(int i=1;i<=m;i++)
		cout<<ans[i]<<'\n';
	return 0;
}
```