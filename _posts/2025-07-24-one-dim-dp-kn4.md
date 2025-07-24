---
layout: post
title: "一维 dp 中的斜率优化与四边形不等式"
tags: 笔记 算法
---

斜率优化：

$$
f_i=\min_{j<i}f_j+w(i,j)+与j无关的量\\
w(i,j)=a_ik_j+b_j
$$

这样，就相当于之前有若干条线段，斜率为 $k_j$，截距为 $b_j$，使用 lich 树找到之前最小的那根线段即可。  
在有 lich 树的情况下好想又好写。

P3195 [HNOI2008] 玩具装箱
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
struct pdi{double fi;int se;};
mt19937_64 rng(random_device{}());
constexpr int N=5e4+1;
constexpr loli inf=0x3f3f3f3f3f3f3f3f;
int n,L,a[N];
loli f[N],s[N];
constexpr double eps=1e-9;
struct lich{
	using pdd=pair<double,double>;
	using pdl=pair<double,loli>;
	vector<pdd>b;
	static int cmp(double x,double y){
		if(x-y>eps)return 1;
		if(y-x>eps)return -1;
		return 0;
	}
	struct node{
		node *ls=nullptr,*rs=nullptr;
		int id=0;
	}*rt=new node;
	double calc(int id,loli x){
		return b[id].fi*x+b[id].se;
	}
	#define mid ((l+r)>>1)
	void mark(node*&u,loli l,loli r,int id1){
		if(l>r)return;
		if(!u)u=new node;
		int&id2=u->id;
		int bmid=cmp(calc(id1,mid),calc(id2,mid));
		if(bmid==1||(!bmid&&id1<id2))swap(id1,id2);
		int bl=cmp(calc(id1,l),calc(id2,l)),br=cmp(calc(id1,r),calc(id2,r));
		if(bl==1||(!bl&&id1<id2))mark(u->ls,l,mid,id1);
		if(br==1||(!br&&id1<id2))mark(u->rs,mid+1,r,id1);
	}
	void update(node*&u,loli l,loli r,loli x,loli y,int id){
		if(!u)u=new node;
		if(x<=l&&r<=y)return mark(u,l,r,id);
		if(x<=mid)update(u->ls,l,mid,x,y,id);
		if(y>mid)update(u->rs,mid+1,r,x,y,id);
	}
	pdl query(node*&u,int l,int r,int x){
		if(!u)u=new node;
		pdl res={calc(u->id,x),u->id};
		if(l==r)return res;
		return max(res,x<=mid?query(u->ls,l,mid,x):query(u->rs,mid+1,r,x),
			[](const pdl&x,const pdl&y){
				if(cmp(x.fi,y.fi)!=0)return x.fi<y.fi;
				return x.se>y.se;
			});
	}
	void add(loli x1,loli y1,loli x2,loli y2){
		if(x1==x2)b.emplace_back(0,max(y1,y2));
		else{
			double k=(1.*y2-y1)/(x2-x1);
			b.emplace_back(k,y1-k*x1);
		}
		update(rt,-inf,inf,x1,x2,siz(b)-1);
	}
	void add(loli x1,loli y1){
		b.emplace_back(x1,y1);
		update(rt,-inf,inf,-inf,inf,siz(b)-1);
	}
	int ask(loli x){
		return query(rt,-inf,inf,x).se;
	}
}tr;
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>L;L++;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		s[i]=s[i-1]+a[i]+1;
	}
	tr.add(-inf,-1ll*L*L,inf,-1ll*L*L);
	for(int i=1;i<=n;i++){
		int j=tr.ask(-2*s[i]);
		auto sqr=[](auto x){return x*x;};
		f[i]=f[j]+sqr(s[i]-s[j]-L);
		tr.add(-s[i],-(sqr(s[i]+L)+f[i]));
	}
	cout<<f[n];
	return 0;
}
```

决策单调：
如果决策单调，即最优转移点 $j$ 随着 $i$ 的上升满足单调不降，即具有决策单调性。  

$$
f_i=w(i,j)
$$

如果 $w(i,j)$ 与 $j$ 无关，即可使用分治维护决策点。  
即每次对于当前询问 $[l,r]$，已知该区间的决策点均在区间 $[x,y]$ 内，不妨对于询问 $mid$ 暴力跑出其决策点 $pos$，那么 $[l,mid-1]$ 的决策点均在 $[x,pos]$，$[mid+1,r]$ 的决策点均在 $[pos,y]$。

P3515 [POI 2011] Lightning Conductor
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
constexpr int N=5e5+7;
int n,h[N];
double f[N];
#define mid ((l+r)>>1)
void solve(int l,int r,int x,int y){
	if(l>r)return;
	int pos=-1;double tmp=-1e9;
	for(int k=x;k<=y&&k<mid;k++)
		if(tmp<h[k]+sqrt(mid-k)-h[mid]){
			tmp=h[k]+sqrt(mid-k)-h[mid];
			pos=k;
		}
	f[mid]=max(f[mid],tmp);
	solve(l,mid-1,x,pos);
	solve(mid+1,r,pos,y);
}
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n;
	for(int i=1;i<=n;i++)cin>>h[i];
	solve(1,n,1,n);
	reverse(f+1,f+1+n);
	reverse(h+1,h+1+n);
	solve(1,n,1,n);
	for(int i=n;i;i--)
		cout<<int(ceil(f[i]))<<'\n';
	return 0;
}
```

四边形不等式：如果 $a<b<c<d$，均有 $w(a,c)+w(b,d)\le w(a,d)+w(b,c)$，则称转移满足四边形不等式。  
当满足四边形不等式时，必然满足决策单调性。此时如果 $w(i,j)$ 与 $j$ 无关，仍然采取分治做法，否则得采取一个二分单调队列。  
代码没意思，不如直接贺，不同题目只有函数 $w$ 要改。

P3195 [HNOI2008] 玩具装箱
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
constexpr int N=5e4+7;
int n,L,a[N];
loli s[N],f[N];
struct node{
	int p,l,r;
};
deque<node>q;
signed main(){
//	freopen(".in","r",stdin);
//	freopen(".out","w",stdout);
	ios::sync_with_stdio(false);cin.tie(nullptr);
	cin>>n>>L;
	for(int i=1;i<=n;i++){
		cin>>a[i];
		s[i]=s[i-1]+a[i];
	}
	auto W=[](int l,int r){
		auto tmp=s[r]-s[l]+r-l-1-L;
		return f[l]+tmp*tmp;
	};
	q.emplace_back(0,1,n);
	for(int i=1;i<=n;i++){
		while(!q.empty()&&q.front().r<i)q.pop_front();
		f[i]=W(q.front().p,i);
		while(!q.empty()&&W(i,q.back().l)<=W(q.back().p,q.back().l))q.pop_back();
		int l=q.back().l,r=n,pos=n+1;
#define mid ((l+r)>>1)
		while(l<=r){
			if(W(i,mid)<=W(q.back().p,mid))
				pos=mid,r=mid-1;
			else l=mid+1;
		}
		if(pos>n)continue;
		q.back().r=pos-1;
		q.emplace_back(i,pos,n);
	}
	cout<<f[n];
	return 0;
}
```