---
abbrlink: ''
author: zyuan
categories:
- - acmer之路
date: '2025-10-14T20:21:30.613083+08:00'
excerpt: CQOI 扑克牌  链接: https://ac.nowcoder.com/acm/problem/...
tags:
- 二分答案
title: '刷题 : CQOI 扑克牌'
updated: '2025-10-14T20:36:04.794+08:00'
---
## CQOI 扑克牌

> 链接: https://ac.nowcoder.com/acm/problem/19916

## 题目描述

> ​	$\hspace{15pt}$本题转译自 [CQOI2010] 扑克牌。

$\hspace{15pt}$你有 $n$ 种牌，第 $i$ 种牌的数目为 $c_i$ 。另外有 $m$ 张特殊的 $\texttt{Joker}$ 牌。你有如下方法来组成一套牌：
$\hspace{23pt}\bullet\,$不使用 $\texttt{Joker}$ 牌，$n$ 种牌各一张;
$\hspace{23pt}\bullet\,$使用一张 $\texttt{Joker}$ 牌，其他 $n-1$ 种牌各一张;
$\hspace{15pt}$比如，当 $n=3$ 时，一共有四种不同的组合方式：$\{1,2,3\}$、 $\{\texttt{Joker},2,3\}$、 $\{\texttt{Joker},1,3\}$、 $\{\texttt{Joker},1,2\}$。
$\hspace{15pt}$现在，给出 $n, m$ 和 $c_i$，你的任务是组成尽量多套牌。每张牌最多只能用在一副套牌里（可以有牌不使用）。

### 输入描述:

> 第一行输入两个整数 n,m(2≤n≤50; 0≤m≤ $5×10^8 $) 代表牌的种数和 Joker的个数。
> 
> 第二行输入 $n$ 个整数 $c_1, c_2, \cdots, c_n \left(0 \leq c_i \leq 5 \times 10^8 \right)$ 代表每种牌的张数

### 输出描述:

```
在一行上输出一个整数，代表最多可以组出几套牌。
```

### 输入

```
3 4
1 2 3
```

### 输出

```
3
```





## 解题思路

乍一看挺难, 好像贪心也不知道怎么做

不过想了下, 感觉可以枚举(其实我看到了那个标签写了个二分), 然后就一下子想到二分答案了.

check(x) 的思路是这样, 因为一共不是 n 种牌吗, 然后就用万能牌补, 但是万能牌 补的数量有限制

- 每套牌, 万能牌的数量不能超过 1 , 所以总数不能超过 x - 1
- 万能牌的数量不能超过 m

然后用二分模版进行压缩 (这个板子好像有点问题, 不过就是 l 的 位置和 r 的位置, 自己理解一下适当交换即可)

果然还是不要抄板子, 尽可能自己写比较好. (哦对, 这个题还卡 long long )

```cpp
bool check(){};
int bsearch(int l ,int r ){
     int ans;
     while(l <= r ){ // 上面就是 l <= r 了, 和二分查找板子有所不同
       int mid =  l + r >> 1;
       if (check() <= x ){ // 这里一定是满足条件, 再记录, 
         ans  = mid;
         r = m - 1;
       }else {
         l = m + 1;
     }return ans;
}
```

## ac 代码

```cpp
#include <bits/stdc++.h>
using namespace std;
#define int long long
const int N = 55;
int card[N];
int n, m;
const int inf = 2e9;
bool check(int x)
{
    int cnt = 0;
    for (int i = 1; i <= n; i++)
    {
        if (card[i] < x)
            cnt += x - card[i]; // 缺少的话就要补牌
    }
    return cnt <= m && cnt <= x; // 补牌数不能超过m , 而且每套只能用一张万能牌
}
int bin_search(int l, int r)
{
    int ans;
    while (l <= r)
    {
        int mid = l + r >> 1;
        // cout << " mid = " << mid << endl;
        if (check(mid))
        {
            // cout << "ans = " << mid << endl;
            ans = mid;
            l = mid  + 1 ;
        }
        else
            r = mid - 1;
    }
    return ans;
}
signed main()
{
    cin >> n >> m;
    int r = -inf;
    for (int i = 1; i <= n; i++)
    {
        cin >> card[i];
        r = max(r, card[i]);
    }
    // cout << r << endl;
    cout << bin_search(0, r + m) << "\n";
}
```


