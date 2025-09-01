---
abbrlink: catch that cow
author: zzhaire
categories:
- - acmer之路
date: '2025-09-01T22:31:52.735665+08:00'
tags:
- bfs
- 搜索
title: Catch That Cow
updated: '2025-09-01T22:31:52.902+08:00'
---
## 题目链接

> https://vjudge.net/problem/POJ-3278

## 题目描述

Farmer John has been informed of the location of a fugitive cow and wants to catch her immediately. He starts at a point *N* (0 ≤ *N* ≤ 100,000) on a number line and the cow is at a point *K* (0 ≤ *K* ≤ 100,000) on the same number line. Farmer John has two modes of transportation: walking and teleporting.

\* Walking: FJ can move from any point *X* to the points *X *- 1 or *X *+ 1 in a single minute
\* Teleporting: FJ can move from any point *X* to the point 2 × *X* in a single minute.

If the cow, unaware of its pursuit, does not move at all, how long does it take for Farmer John to retrieve it?

### Input

Line 1: Two space-separated integers: *N* and *K*

### Output

Line 1: The least amount of time, in minutes, it takes for Farmer John to catch the fugitive cow.

### Sample

| Input    | Output |
| -------- | ------ |
| `5 17` | `4`  |

### Hint

The fastest way for Farmer John to reach the fugitive cow is to move along the following path: 5-10-9-18-17, which takes 4 minutes.

## 思路

> 题目意思大概是 有一个农夫, 农夫在一个点上面, 能做的操作有 乘以2 , 或者 + 1 , - 1 , 然后要到达另一个点, 求最少的操作次数
>
> 一开始想着贪心乘法, 然后再尝试 + 1  ,  -1 去移动到关键位置, 后面看了下测试样例, 发现没有规律

不过正常BFS的话, 肯定要超时, 不过好在可以记录VIS[] 确保快速剪肢, 整体时间复杂度不会超过数组长度, 大概是1e6的大小, 时间复杂度为$O(n)$ .

然后也是bfs 的写法, 这里需要枚举好下一个状态进入节点

## AC 代码

```cpp
#include <iostream>
#include <vector>
#include <queue>
using namespace std;
int n, k;
int ans;
const int N = 1e6 + 10;
int vis[N];
#define x first
#define y second
typedef pair<int, int> pii;
int bfs()
{
    queue<pii> q;
    pii tmp;
    tmp.x = n;
    tmp.y = 0;
    q.push(tmp);
    while (q.size())
    {
        tmp = q.front();
        q.pop();
        int t = tmp.x, step = tmp.y;
        // cout <<"debug" << t << " " << step << endl;
        if (t == k)
            return step;
        int t1 = t + 1;
        pii nt;
        nt.x = t1, nt.y = step + 1;
        if (t1 >=0 && t1 <= N && !vis[t1])
            vis[t1] = 1, q.push(nt);

        int t2 = t - 1;
        nt.x = t2;
        if (t2 >=0 && t2 <= N && !vis[t2])
            vis[t2] = 1, q.push(nt);

        int t3 = t * 2;
        nt.x = t3;
        if (t3 >=0 && t3 <= N && !vis[t3])
            vis[t3] = 1, q.push(nt);
    }
    return -1;
}
signed main()
{
    cin >> n >> k;
    cout << bfs() << endl;
}
```

## 其他

做了第三道搜索题了,感觉基本上最短路径就是用BFS搜索

然后整个代码基本上就是

```cpp
q.push(初始节点)
while(q.size())
{
    auto t = q.front() ; q.pop();
    for( next : 下一个状态)
    {
         if(!满足剪肢)
             q.push(next);
    }
}
```

具体情况具体题目决定, 有时候要在节点里记录步长.
