---
title: 【Ynoi#33】【Ynoi2014】不归之人与望眼欲穿的人们
date: 2023-12-28 21:45:46
tags: OI
categories: Ynoi
mathjax: enable
---


首先有一个经典的结论，就是对于固定的右端点，or 和的不同的值最多只有 $O(\log a)$ 个。

考虑分块，对于每个整块，维护前缀和后缀的所有不同的 or 和。

对于跨越块的区间，每次查询从左向右扫，记录前 $k-1$ 个块的后缀不同 or 和，然后用这个后缀和第 $k$ 个块的前缀做一个双指针计算答案，然后将前 $k-1$ 个块的后缀 or 上第 $k$ 个块，再将第 $k$ 个块内的后缀加入更新去重即可。

对于块内的部分，我们用 $f(len)$ 表示长度 $\leq len$ 的区间中 or 和最大的是多少，每次询问二分即可。

对于修改，我们暴力重构一个块即可。

注意在块内 $f(len)$ 的部分，对于每个右端点计算 $O(\log a)$ 个左区间的时候，实际上就是对于每一位求 $\leq i$ 的第一个 1，这部分如果额外排序的话就会损失一个 $\log \log a$。所以我们从左往右推的时候用队列维护一下这个顺序就可以了，因为除了 $a_i$ 是 $1$ 的那些为其他位变成 $1$ 的顺序和 $i-1$ 是一样的。

复杂度 $O(n\sqrt n\log a)$

```cpp
#include <bits/stdc++.h>

using namespace std;

# define Rep(i,a,b) for(int i=a;i<=b;i++)
# define _Rep(i,a,b) for(int i=a;i>=b;i--)
# define RepG(i,u) for(int i=head[u];~i;i=e[i].next)

const int N=50005;
const int M=135;

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
int a[N];
int L[N],R[N],pos[N],sq=400,bl;
PII res[66];
int len;
int orsum[M];
int mx[M][405];
int lenp[M],lens[M];
PII pre[M][33],suf[M][33];
PII myq[23333],cach[66];

void rebuild(int x){
    memset(mx[x],0,sizeof(mx[x]));
    lenp[x]=lens[x]=0;
    int tmp=0;
    Rep(i,L[x],R[x]) if((tmp|a[i])!=pre[x][lenp[x]].first)tmp|=a[i],pre[x][++lenp[x]]=mkp(tmp,i);
    tmp=0;
    _Rep(i,R[x],L[x])if((tmp|a[i])!=suf[x][lens[x]].first)tmp|=a[i],suf[x][++lens[x]]=mkp(tmp,i);
    int head=1,tail=0;
    Rep(i,L[x],R[x]){
        int lst=tail;
        for(int j=a[i];j;j-=j&-j)myq[++tail]=mkp(__builtin_ctz(j),i);
        for(int j=head;j<=lst;j++)if(!(a[i]>>myq[j].first&1))myq[++tail]=myq[j];
        head=lst+1;
        tmp=0;
        Rep(j,head,tail){
            tmp|=a[myq[j].second];
            chkmax(mx[x][i-myq[j].second+1],tmp);
        }
    }
    Rep(i,2,R[x]-L[x]+1)chkmax(mx[x][i],mx[x][i-1]);
    orsum[x]=0;
    Rep(i,L[x],R[x])orsum[x]|=a[i];
}

void maintain(){
    Rep(i,2,len)if(res[i].first==res[i-1].first)res[i].second=res[i-1].second;
    len=unique(res+1,res+len+1)-res-1;
}

void merge(int x){
    int i=1,j=1,it=1;
    while(i<=len&&j<=lens[x])
        if(res[i].first<suf[x][j].first)cach[it++]=res[i++];
        else cach[it++]=suf[x][j++];
    while(i<=len)cach[it++]=res[i++];
    while(j<=lens[x])cach[it++]=suf[x][j++];
    it--;
    len=it;
    Rep(i,1,len)res[i]=cach[i];
    maintain();
}

int calc(int x,int k){
    int ans=1e9+114514;
    Rep(i,1,lenp[x])
        while(len&&(res[len].first|pre[x][i].first)>=k)
            chkmin(ans,pre[x][i].second-res[len].second+1),len--;
    return ans;
}

int main()
{
    # ifndef ONLINE_JUDGE
    freopen("testdata.in","r",stdin);
    //freopen("test1.out","w",stdout);
    # endif
    read(n),read(m);
    Rep(i,1,n)read(a[i]);
    Rep(i,1,n)pos[i]=(i-1)/sq+1;
    bl=pos[n];
    Rep(i,1,bl)L[i]=(i-1)*sq+1,R[i]=i*sq;
    R[bl]=n;
    Rep(i,1,bl)rebuild(i);
    Rep(i,1,m){
        int opt,x,y;
        read(opt),read(x);
        if(opt==1){
            read(y);
            a[x]=y;
            rebuild(pos[x]);
        }
        else{
            int ans=1e9+114514;
            Rep(i,1,bl)if(orsum[i]>=x)chkmin(ans,(int)(lower_bound(mx[i]+1,mx[i]+R[i]-L[i]+2,x)-mx[i]));
            len=0;
            merge(1);
            Rep(i,2,bl){
                chkmin(ans,calc(i,x));
                Rep(j,1,len)res[j].first|=orsum[i];
                maintain();
                merge(i);
            }
            if(ans>1e9)puts("-1");
            else printf("%d\n",ans);
        }   
    }
    return 0;
}
```