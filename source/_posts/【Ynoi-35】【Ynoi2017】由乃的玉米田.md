---
title: 【Ynoi#35】【Ynoi2017】由乃的玉米田
date: 2023-12-31 17:54:58
tags: OI
categories: Ynoi
mathjax: enable
---

莫队加 bitset 解决前三个操作

第四个操作在 $x>\sqrt n$ 的时候同样解决了。

$x\leq \sqrt n$ 的时候，对于 $x$ 相同的放在一起处理，设 $f[i]$ 表示最大的 $j$ 满足 $[i,j]$ 中有一对商是 $x$ 的，不难转移。

复杂度 $O(n\sqrt n)$

```cpp
# include <bits/stdc++.h>

using namespace std;

# define Rep(i,a,b) for(int i=a;i<=b;i++)
# define _Rep(i,a,b) for(int i=a;i>=b;i--)
# define RepG(i,u) for(int i=head[u];~i;i=e[i].next)

typedef long long ll;
typedef double db;

# define chkmax(a,b) a=max(a,b)
# define chkmin(a,b) a=min(a,b)
# define PII pair<int,int>
# define mkp make_pair

const int N=1e5+5;

template<typename T> void read(T &x){
    x=0;int f=1;
    char c=getchar();
    for(;!isdigit(c);c=getchar())if(c=='-')f=-1;
    for(;isdigit(c);c=getchar())x=(x<<1)+(x<<3)+c-'0';
    x*=f;
}

int n,m;
int a[N];
int pos[N],sq;
int cnt[N];
int lst[N],f[N];
int out[N];
int lim=300;
int qcnt;

bitset<N> S,SI;

struct misaka{
    int opt,l,r,x,id;
}Q[N];

vector<misaka> T[305];

bool cmp(misaka x,misaka y){
    if(pos[x.l]!=pos[y.l])return pos[x.l]<pos[y.l];
    else if(pos[x.l]&1)return x.r<y.r;
    else return x.r>y.r;
}

void ins(int x){
    if(!cnt[x])S[x]=1,SI[100000-x]=1;
    cnt[x]++;
}

void del(int x){
    cnt[x]--;
    if(!cnt[x])S[x]=0,SI[100000-x]=0;
}

int main()
{
    # ifndef ONLINE_JUDGE
    freopen("testdata.in","r",stdin);
    //freopen("test1.out","w",stdout);
    # endif
    read(n),read(m);
    Rep(i,1,n)read(a[i]);
    sq=sqrt(n)+1;
    Rep(i,1,n)pos[i]=(i-1)/sq+1;
    Rep(i,1,m){
        int opt,x,l,r;
        read(opt),read(l),read(r),read(x);
        if(opt==4&&x<=lim)T[x].push_back((misaka){4,l,r,x,i});
        else Q[++qcnt]=(misaka){opt,l,r,x,i};
    }
    sort(Q+1,Q+qcnt+1,cmp);
    for(int i=1,l=1,r=0;i<=qcnt;i++){
        while(l>Q[i].l)ins(a[--l]);
        while(r<Q[i].r)ins(a[++r]);
        while(l<Q[i].l)del(a[l++]);
        while(r>Q[i].r)del(a[r--]);
        if(Q[i].opt==1)out[Q[i].id]=((S<<Q[i].x)&S).any();
        else if(Q[i].opt==2)out[Q[i].id]=((S<<(100000-Q[i].x))&SI).any();
        else if(Q[i].opt==3){
            for(int j=1;j*j<=Q[i].x;j++)
                if(Q[i].x%j==0&&S[j]&&S[Q[i].x/j])
                    out[Q[i].id]=true;
        }
        else{
            for(int j=1;j*Q[i].x<=100000;j++)
                if(S[j]&&S[j*Q[i].x])
                    out[Q[i].id]=true;
        }
    }
    Rep(x,1,lim){
        if(T[x].empty())continue;
        Rep(i,1,n){
            int y=a[i];
            lst[y]=i;
            f[i]=f[i-1];
            if(x*y<=100000)chkmax(f[i],lst[x*y]);
            if(y%x==0)chkmax(f[i],lst[y/x]);
        }
        for(auto i:T[x])
            out[i.id]=i.l<=f[i.r];
        memset(f,0,sizeof(f));
        memset(lst,0,sizeof(lst));
    }
    Rep(i,1,m)puts(out[i]?"yuno":"yumi");
    return 0;
}
```