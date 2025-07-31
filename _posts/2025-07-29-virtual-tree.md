---
layout: post
title: "虚树速通"
tags: 笔记 算法
---

如果每次询问是输入树上一个点集，那么做法往往是虚树。  
虚树就是把原图中所有有用的点抠出来，然后把抠出来的点建颗树，叫虚树。  
那哪些点有用？`b` 中的点是输入的点（关键点），`c` 中的点是有用的点（为了可以树形 dp 不得不加入的点）。  
其实虚树就相当于把一棵树中两个关键点路径间的点压缩成了很少的几个点，把不在关键点路径上的都忽略掉了。
```cpp
int m;cin>>m;
b.resize(m);
for(int i=0;i<m;i++)cin>>b[i];
std::sort(all(b),[](int x,int y){
	return dfn[x]<dfn[y];
});
c=b;
for(int i=1;i<m;i++)
	c.push_back(LCA(b[i-1],b[i]));
sort(all(c),[](int x,int y){
	return dfn[x]<dfn[y];
});
c.erase(unique(all(c)),c.end());
for(int i=1;i<siz(c);i++){
	int j=LCA(c[i-1],c[i]),d=DIS(j,c[i]);
	g2[j].emplace_back(c[i],d);
	g2[c[i]].emplace_back(j,d);
}
```

P4103 [HEOI2014] 大工程

每次询问给出若干关键点，求所有关键点形成的路径的权值和，距离最近的关键点和距离最远的关键点。

权值和只需对虚树上一条边上下 `siz` 乘一下即可。
距离最近的关键点和距离最远的关键点只需在某对点的 LCA 合并处计算贡献即可，即对于每个点 $u$，记录 $u$ 儿子中最远的两个关键点和最近的两个关键点。

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
constexpr int N=1e6+1,inf=0x3c3c3c3c;
loli sum;
int n,Q,ans1,ans2;
int fa[N],sz1[N],dep[N],top[N],dfn[N],gs[N];
int sz2[N],mn[N],mx[N];
std::vector<int>g1[N];
std::vector<pii>g2[N];
std::vector<int>b,c;
bool ess[N];
void dfs1(int u){
	for(int v:g1[u])if(v!=fa[u]){
		fa[v]=u;
		sz1[v]=1;
		dep[v]=dep[u]+1;
		dfs1(v);
		sz1[u]+=sz1[v];
		if(sz1[v]>sz1[gs[u]])gs[u]=v;
	}
}
void dfs2(int u,int t){
	static int dfn_cnt=0;
	top[u]=t;dfn[u]=++dfn_cnt;
	if(!gs[u])return;
	dfs2(gs[u],t);
	for(int v:g1[u])if(v!=fa[u]&&v!=gs[u])
		dfs2(v,v);
}
int LCA(int x,int y){
	for(;top[x]!=top[y];x=fa[top[x]])
		if(dep[top[x]]<dep[top[y]])
			std::swap(x,y);
	return dep[x]<dep[y]?x:y;
}
int DIS(int x,int y){
	return dep[x]+dep[y]-2*dep[LCA(x,y)];
}
void dfs3(int u,int fa){
	if(ess[u]){
		sz2[u]=1;
		mn[u]=mx[u]=0;
	}else{
		sz2[u]=0;
		mn[u]=inf;
		mx[u]=-inf;
	}
	int mn2=inf,mx2=-inf;
	for(auto[v,w]:g2[u])if(v!=fa){
		dfs3(v,u);
		sum+=1ll*w*sz2[v]*(siz(b)-sz2[v]);
		sz2[u]+=sz2[v];
		int z=mn[v]+w;
		if(z<mn[u])mn2=mn[u],mn[u]=z;
		else mn2=min(mn2,z);
		z=mx[v]+w;
		if(z>mx[u])mx2=mx[u],mx[u]=z;
		else mx2=max(mx2,z);
	}
	ans1=min(ans1,mn[u]+mn2);
	ans2=max(ans2,mx[u]+mx2);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	std::ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n;
	for(int i=1,u,v;i<n;i++){
		cin>>u>>v;
		g1[u].push_back(v);
		g1[v].push_back(u);
	}
	dfs1(1);dfs2(1,1);
	cin>>Q;
	for(;Q--;){
		sum=0;ans1=inf;ans2=-inf;
		int m;cin>>m;
		b.resize(m);
		for(int i=0;i<m;i++)cin>>b[i];
		std::sort(all(b),[](int x,int y){
			return dfn[x]<dfn[y];
		});
		c=b;
		for(int i=1;i<m;i++)
			c.push_back(LCA(b[i-1],b[i]));
		sort(all(c),[](int x,int y){
			return dfn[x]<dfn[y];
		});
		c.erase(unique(all(c)),c.end());
		for(int i=1;i<siz(c);i++){
			int j=LCA(c[i-1],c[i]),d=DIS(j,c[i]);
			g2[j].emplace_back(c[i],d);
			g2[c[i]].emplace_back(j,d);
		}
		for(int i:b)ess[i]=true;
		dfs3(c[0],0);
		for(int i:c)g2[i].clear(),ess[i]=false;
		cout<<sum<<' '<<ans1<<' '<<ans2<<'\n';
	}
	return 0;
}
```

P4606 [SDOI2018] 战略游戏

本题有点烦，建出圆方树后，相当于每次询问给出若干关键点，问有多少圆点能被关键点形成的路径经过。  
再次建虚树后 `dfs` 算贡献即可。  
具体地说，由于虚树上的点要么是关键点，要么是关键点的 LCA 必然在关键点的路径上，所以虚树上的每个圆点都是有贡献的。  
对于其余圆点，只需要在圆方树上跑一个树上前缀和，用于计算圆方树上两点之间圆点数量，那么就可以对虚树上每条边去计算贡献了。如果虚树上某条边的两个点两侧均有关键点，那么贡献是该边被压缩前的圆点数量，否则没有贡献。  
记得写的时候千万不能把 tarjan 的 dfn 用于建虚树，因为建圆方树后会产生新的方点，需要在建圆方树后跑出新的 dfn。
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
constexpr int N=2e5+7;
int n1,m,n2,q,dc,dfn[N],low[N];
int cnt,ans,pre[N];
int ffa[N],top[N],gs[N],sz[N],dep[N];
stack<int>s;
basic_string<int>g1[N],g2[N],g3[N];
vector<int>b,c;
void tar3(int u){
	dfn[u]=low[u]=++dc;
	s.push(u);
	auto add=[](int x,int y){g2[x]+=y;g2[y]+=x;};
	for(int v:g1[u])
		if(!dfn[v]){
			tar3(v);
			low[u]=min(low[u],low[v]);
			if(low[v]>=dfn[u]){
				n2++;
				for(;s.top()!=v;s.pop())add(s.top(),n2);
				s.pop();
				add(n2,u);add(n2,v);
			}
		}else low[u]=min(low[u],dfn[v]);
}
void dfs_qwq(int u,int fa){
	for(int v:g3[u])if(v!=fa){
		dfs_qwq(v,u);
	}
	for(int v:g3[u])if(v!=fa){
		int w=pre[v]-pre[u];
		if(v<=n1)w--;
		ans+=w;
	}
}
void dfs1(int u){
	sz[u]=1;
	gs[u]=0;top[u]=0;
	dfn[u]=++dc;
	if(u==1)pre[u]=1;
	for(int v:g2[u]){
		if(v==ffa[u])continue;
		ffa[v]=u,dep[v]=dep[u]+1;
		pre[v]=pre[u]+(v<=n1);
		dfs1(v);sz[u]+=sz[v];
		if(sz[v]>sz[gs[u]])gs[u]=v;
	}
}
void dfs2(int u,int t){
	top[u]=t;
	if(!gs[u])return;
	else dfs2(gs[u],t);
	for(int v:g2[u])if(v!=ffa[u]&&v!=gs[u])
		dfs2(v,v);
}
int LCA(int x,int y){
	for(;top[x]!=top[y];x=ffa[top[x]])
		if(dep[top[x]]<dep[top[y]])swap(x,y);
	return dep[x]<dep[y]?x:y;
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	int T;cin>>T;while(T--){
		cin>>n1>>m;n2=n1;
		for(int i=1,u,v;i<=m;i++)
			cin>>u>>v,g1[u]+=v,g1[v]+=u;
		for(int i=1;i<=n1;i++)
			if(!dfn[i])tar3(i);
		dc=0;
		dfs1(1);dfs2(1,1);
		cin>>q;for(;q--;){
			cin>>cnt;
			ans=0;
			b.resize(cnt);
			for(int i=0;i<siz(b);i++)cin>>b[i];
			sort(all(b),[](int x,int y){
				return dfn[x]<dfn[y];
			});
			c=b;
			for(int i=1;i<siz(b);i++)
				c.push_back(LCA(b[i-1],b[i]));
			sort(all(c),[](int x,int y){
				return dfn[x]<dfn[y];
			});
			c.erase(unique(all(c)),c.end());
			for(int i=1;i<siz(c);i++){
				int j=LCA(c[i-1],c[i]);
				g3[j].push_back(c[i]);
				g3[c[i]].push_back(j);
			}
			dfs_qwq(c[0],0);
			for(int i:c)if(i<=n1)ans++;
			cout<<ans-siz(b)<<'\n';
			for(int i=1;i<siz(c);i++){
				int j=LCA(c[i-1],c[i]);
				g3[j].clear();
				g3[c[i]].clear();
			}
		}
		dc=0;
		for(int i=1;i<=n2;i++){
			g1[i].clear();
			low[i]=dfn[i]=0;
			g2[i].clear();
		}
	}
	return 0;
}
```