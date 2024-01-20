---
title: 【Ynoi#34】【Ynoi2017】由乃的OJ
date: 2023-12-30 17:44:15
tags: OI
categories: Ynoi
mathjax: enable
---


首先注意到每一位是独立的，只需要枚举 $0$ 进去还是 $1$ 进去对应的就可以算出来。

这个不难用树剖线段树/LCT 维护，得到 3log 的做法。

然后可以用一个 unsigned long long 把每一位压到一起，然后就 2log(1log) 了。

```cpp
#include <bits/stdc++.h>

using namespace std;

# define Rep(i,a,b) for(int i=a;i<=b;i++)
# define _Rep(i,a,b) for(int i=a;i>=b;i--)
# define RepG(i,u) for(int i=head[u];~i;i=e[i].next)

const int N=1e5+5;
const unsigned long long inf=0-1;

# define ll long long
# define db double
# define ull unsigned long long
# define uint unsigned int
# define chkmax(a,b) a=max(a,b)
# define chkmin(a,b) a=min(a,b)
# define mkp make_pair
# define PII pair<int,int>
# define PLL pair<ll,ll>
# define PIL pair<int,ll>
# define PLI pair<ll,int>

template<typename T> void read(T &x){
    x=0;int f=1;
    char c=getchar();
    for(;!isdigit(c);c=getchar())if(c=='-')f=-1;
    for(;isdigit(c);c=getchar())x=(x<<1)+(x<<3)+c-'0';
    x*=f;
}

int n,m,bit;
int head[N],cnt;
int o[N];
ull a[N];
int dfn[N],siz[N],_a[N],top[N],dep[N],faz[N],son[N],dfsxu;

struct Edge{
    int to,next;
}e[N<<1];

void add(int x,int y){
    e[++cnt]=(Edge){y,head[x]},head[x]=cnt;
}

struct node{
    ull l0,l1,r0,r1;
    node(){l0=r0=0,l1=r1=inf;}
}seg[N<<2];

void dfs1(int u,int fa){
    faz[u]=fa,dep[u]=dep[fa]+1;
    siz[u]=1;
    RepG(i,u){
        int v=e[i].to;
        if(v==fa)continue;
        dfs1(v,u);
        siz[u]+=siz[v];
        if(siz[v]>siz[son[u]])son[u]=v;
    }
}

void dfs2(int u,int _top){
    dfn[u]=++dfsxu;
    _a[dfsxu]=u;
    top[u]=_top;
    if(!son[u])return;
    dfs2(son[u],_top);
    RepG(i,u){
        int v=e[i].to;
        if(v==faz[u]||v==son[u])continue;
        dfs2(v,v);
    }
}

# define lc (u<<1)
# define rc (u<<1|1)

ull calc(ull x,int p){
    if(o[p]==1)return x&a[p];
    if(o[p]==2)return x|a[p];
    if(o[p]==3)return x^a[p];
}

node merge(node x,node y){
    node res;
    res.l0=(x.l0&y.l1)|((~x.l0)&y.l0); 
    res.l1=(x.l1&y.l1)|((~x.l1)&y.l0);
    res.r0=(y.r0&x.r1)|((~y.r0)&x.r0);
    res.r1=(y.r1&x.r1)|((~y.r1)&x.r0);
    return res;
}

void build(int u,int l,int r){
    if(l==r){
        seg[u].l0=seg[u].r0=calc(0,_a[l]);
        seg[u].l1=seg[u].r1=calc(inf,_a[l]);
        return;
    }
    int mid=l+r>>1;
    build(lc,l,mid);
    build(rc,mid+1,r);
    seg[u]=merge(seg[lc],seg[rc]);  
}

void update(int u,int l,int r,int x){
    if(l==r){
        seg[u].l0=seg[u].r0=calc(0,_a[l]);
        seg[u].l1=seg[u].r1=calc(inf,_a[l]);
        return;
    }
    int mid=l+r>>1;
    if(x<=mid)update(lc,l,mid,x);
    else update(rc,mid+1,r,x);
    seg[u]=merge(seg[lc],seg[rc]);
}

node query(int u,int l,int r,int ql,int qr){
    if(l>=ql&&r<=qr)return seg[u];
    int mid=l+r>>1;
    if(qr<=mid)return query(lc,l,mid,ql,qr);
    else if(ql>mid)return query(rc,mid+1,r,ql,qr);
    else return merge(query(lc,l,mid,ql,qr),query(rc,mid+1,r,ql,qr));
}

node RouteQuery(int x,int y){
    node l,r;
    while(top[x]!=top[y])
        if(dfn[top[x]]>dfn[top[y]]){
            l=merge(query(1,1,n,dfn[top[x]],dfn[x]),l);
            x=faz[top[x]];
        }
        else{
            r=merge(query(1,1,n,dfn[top[y]],dfn[y]),r);
            y=faz[top[y]];
        }
    if(dfn[x]<dfn[y])r=merge(query(1,1,n,dfn[x],dfn[y]),r);
    else l=merge(query(1,1,n,dfn[y],dfn[x]),l);
    swap(l.l0,l.r0),swap(l.l1,l.r1);
    return merge(l,r);
}

int main()
{
    # ifndef ONLINE_JUDGE
    freopen("testdata.in","r",stdin);
    //freopen("test1.out","w",stdout);
    # endif
    memset(head,-1,sizeof(head));
    read(n),read(m),read(bit);
    Rep(i,1,n)read(o[i]),read(a[i]);
    Rep(i,1,n-1){
        int x,y;
        read(x),read(y);
        add(x,y),add(y,x);
    }
    dfs1(1,0);
    dfs2(1,1);
    build(1,1,n);
    Rep(i,1,m){
        int opt,x,y;
        ull z;
        read(opt),read(x),read(y),read(z);
        if(opt==2){
            o[x]=y;
            a[x]=z;
            update(1,1,n,dfn[x]);
        }
        else{
            node res=RouteQuery(x,y);
            ull ans=0;
            _Rep(i,63,0){
                int v0=(res.l0>>i)&1ull;
                int v1=(res.l1>>i)&1ull;
                if(v0>=v1||((1ull<<i)>z))ans|=(v0?(1ull<<i):0);
                else ans|=(v1?(1ull<<i):0),z-=1ull<<i;
            }
            printf("%llu\n",ans);
        }
    }
    return 0;
}
```