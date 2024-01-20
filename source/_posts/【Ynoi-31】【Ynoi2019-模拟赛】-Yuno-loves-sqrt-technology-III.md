---
title: 【Ynoi#31】【Ynoi2019 模拟赛】 Yuno loves sqrt technology III
date: 2023-12-25 20:13:05
tags: OI
categories: Ynoi
mathjax: enable
---


~~2023年第一道洛谷~~

[题目链接](https://www.luogu.com.cn/problem/P5048)

一句话题意就是静态区间众数出现次数。

分块，先预处理出 $l$ 到 $r$ 块内出现的众数出现次数。

然后考虑散块的部分，对于新添加的一个数，我们查询他在区间里出现的次数即可，但是这样二分带 log。

解决方法对于当前的 $ans$，对于（以右边部分散块为例）一个新的数 $a_k$，找 $a_k$ 前面第 $ans$ 个位置，判断他是否在这个区间内，如果是，$ans:=ans+1$，然后一步一步往前跳。

这样均摊下来每个散块里的位置只会被跳一遍，复杂度 $O((n+m)\sqrt n)$。

应当说是 Ynoi 里面相当简单的一道题，也不卡常。

```cpp
#include <bits/stdc++.h>

using namespace std;

# define Rep(i,a,b) for(int i=a;i<=b;i++)
# define _Rep(i,a,b) for(int i=a;i>=b;i--)
# define RepG(i,u) for(int i=head[u];~i;i=e[i].next)

const int N=5e5+5;
const int M=805;

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
int sq=700,bl,L[N],R[N],pos[N];
vector<int> p[N];
int mode[M][M],cnt[N];
int loc[N];
int ans;

int main()
{
    # ifndef ONLINE_JUDGE
    freopen("testdata.in","r",stdin);
    //freopen("test1.out","w",stdout);
    # endif
    read(n),read(m);
    Rep(i,1,n)read(a[i]),loc[i]=p[a[i]].size(),p[a[i]].push_back(i);
    Rep(i,1,n)pos[i]=(i-1)/sq+1;
    bl=pos[n];
    Rep(i,1,bl)L[i]=(i-1)*sq+1,R[i]=i*sq;
    R[bl]=n;
    Rep(i,1,bl){
        Rep(j,i,bl){
            mode[i][j]=mode[i][j-1];
            Rep(k,L[j],R[j]){
                cnt[a[k]]++;
                chkmax(mode[i][j],cnt[a[k]]);
            }
        }
        Rep(j,L[i],n)cnt[a[j]]=0;
    }
    Rep(i,1,m){
        int x,y;
        read(x),read(y);
        x^=ans,y^=ans;
        if(pos[x]==pos[y]){
            ans=0;
            Rep(j,x,y)cnt[a[j]]++,chkmax(ans,cnt[a[j]]);
            Rep(j,x,y)cnt[a[j]]=0;
            printf("%d\n",ans);
        }
        else{
            ans=mode[pos[x]+1][pos[y]-1];
            Rep(j,x,R[pos[x]]){
                int k=loc[j];
                while(k+ans<p[a[j]].size()&&p[a[j]][k+ans]<=y)ans++;
            }
            Rep(j,L[pos[y]],y){
                int k=loc[j];
                while(k-ans>=0&&p[a[j]][k-ans]>=x)ans++;
            }
            printf("%d\n",ans);
        }
    }
    return 0;
}
```