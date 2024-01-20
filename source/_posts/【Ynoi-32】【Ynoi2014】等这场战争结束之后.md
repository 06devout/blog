---
title: 【Ynoi#32】【Ynoi2014】等这场战争结束之后
date: 2023-12-27 21:42:23
tags: OI
categories: Ynoi
mathjax: enable
---


首先把操作树建出来，然后值域分块。

用可撤销并查集维护连通块，记录每个连通块在每个块中的出现次数。

查询先定位整块，散块只需要在离散化的时候不去重，暴力找即可。

感觉远远没有达到黑的水平。

$O(m\sqrt{n\log n})$

```cpp
#include <bits/stdc++.h>

using namespace std;

# define Rep(i,a,b) for(int i=a;i<=b;i++)
# define _Rep(i,a,b) for(int i=a;i>=b;i--)
# define RepG(i,u) for(int i=head[u];~i;i=e[i].next)

const int N=1e5+5;
const int B=25;

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

int n,m;
PII a[N];
int b[N];
int head[N],ecnt;
int mode[N];
int fa[N],siz[N],stk[N],top;
short cnt[N][B];
int L[N],R[N],pos[N],sq=4000,bl;
int out[N];

struct Edge{
    int to,next;
}e[N<<1];

void add(int x,int y){
    e[++ecnt]=(Edge){y,head[x]},head[x]=ecnt;
}

struct misaka{
    int opt,x,y;
}Q[N];

int find(int x){
    if(fa[x]==x)return x;
    return find(fa[x]);
}

bool merge(int x,int y){
    x=find(x),y=find(y);
    if(x==y)return false;
    if(siz[x]>siz[y])swap(x,y);
    stk[++top]=x;
    fa[x]=y,siz[y]+=siz[x];
    Rep(i,1,bl)cnt[y][i]+=cnt[x][i];
    return true;
}

void rollback(){
    int x=stk[top--],y=fa[x];
    Rep(i,1,bl)cnt[y][i]-=cnt[x][i];
    siz[y]-=siz[x];
    fa[x]=x;
}

int query(int x,int y){
    x=find(x);
    int k=1;
    while(k<=bl&&y>cnt[x][k])y-=cnt[x][k],k++;
    if(k>bl)return -1;
    Rep(i,L[k],R[k])
        if(find(a[i].second)==x){
            y--;
            if(!y)return a[i].first;
        }
}

void dfs(int u){
    bool flag=false;
    if(Q[u].opt==1)flag=merge(Q[u].x,Q[u].y);
    if(Q[u].opt==3)out[u]=query(Q[u].x,Q[u].y);
    RepG(i,u)dfs(e[i].to);
    if(flag)rollback();
}

int main()
{
    # ifndef ONLINE_JUDGE
    freopen("testdata.in","r",stdin);
    //freopen("test1.out","w",stdout);
    # endif
    memset(head,-1,sizeof(head));
    read(n),read(m);
    Rep(i,1,n)fa[i]=i,siz[i]=1;
    Rep(i,1,n)read(a[i].first),a[i].second=i;
    sort(a+1,a+n+1);
    Rep(i,1,n)b[a[i].second]=i;
    Rep(i,1,n)pos[i]=(i-1)/sq+1;
    bl=pos[n];
    Rep(i,1,bl)L[i]=(i-1)*sq+1,R[i]=i*sq;
    R[bl]=n;
    Rep(i,1,n)cnt[i][pos[b[i]]]++;
    int now=0;
    Rep(i,1,m){
        int opt,x,y;
        read(opt),read(x);
        if(opt==1)read(y),Q[i]=(misaka){1,x,y},add(now,i),now=i;
        if(opt==2)now=mode[x];
        if(opt==3)read(y),Q[i]=(misaka){3,x,y},add(now,i),now=i;
        mode[i]=now;
    }
    dfs(0);
    Rep(i,1,m)if(Q[i].opt==3)printf("%d\n",out[i]);
    return 0;
}
```