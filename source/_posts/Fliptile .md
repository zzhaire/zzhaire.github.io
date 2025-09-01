---
abbrlink: '相似题: 牛可乐的翻转游戏'
author: zzhaire
categories:
- - acmer之路
date: '2025-09-01T22:44:10.395052+08:00'
tags:
- 状态压缩
- 枚举
title: Fliptile
updated: '2025-09-01T22:44:10.260+08:00'
---
## 题目链接

> https://vjudge.net/problem/POJ-3279

## 题目描述

Farmer John knows that an intellectually satisfied cow is a happy cow who will give more milk. He has arranged a brainy activity for cows in which they manipulate an *M* × *N* grid (1 ≤ *M* ≤ 15; 1 ≤ *N* ≤ 15) of square tiles, each of which is colored black on one side and white on the other side.

As one would guess, when a single white tile is flipped, it changes to black; when a single black tile is flipped, it changes to white. The cows are rewarded when they flip the tiles so that each tile has the white side face up. However, the cows have rather large hooves and when they try to flip a certain tile, they also flip all the adjacent tiles (tiles that share a full edge with the flipped tile). Since the flips are tiring, the cows want to minimize the number of flips they have to make.

Help the cows determine the minimum number of flips required, and the locations to flip to achieve that minimum. If there are multiple ways to achieve the task with the minimum amount of flips, return the one with the least lexicographical ordering in the output when considered as a string. If the task is impossible, print one line with the word "IMPOSSIBLE".

### Input

Line 1: Two space-separated integers: *M* and *N*
Lines 2..*M*+1: Line *i*+1 describes the colors (left to right) of row i of the grid with *N* space-separated integers which are 1 for black and 0 for white

### Output

Lines 1..*M*: Each line contains *N* space-separated integers, each specifying how many times to flip that particular location.

### Sample

| Input                                                                        | Output                                                         |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------- |
| `4 4`<br />`1 0 0 1`<br />`0 1 1 0`<br />`0 1 1 0`<br /> `1 0 0 1` | `0 0 0 0`<br />`1 0 0 1`<br />`1 0 0 1`<br />`0 0 0 0` |

## 思路

题目意思大概是说,  棋盘上有很多 黑色砖和白色砖 ,然后每次可以翻转一块砖, 但是翻转这个砖之后, 这个砖上下左右都会翻转.  现在要求最少的步数, 翻转得到最后结果.


> 这个题有点像我之前做过的一道题, 牛客的  牛可乐的翻转游戏, 这个题也是状压枚举
>
> 但是那个题只需要求最少步数, 这个题需要记录一下中间结果 , 字典序有点烦人, 一直wa了很久, 后面看到一个题解, 只需要反过来存就行了.


## AC 代码

```cpp
#include <iostream>
#include <cstring>
using namespace std;

const int MAXN = 20;
int input[MAXN][MAXN], op[MAXN][MAXN], ans[MAXN][MAXN], record[MAXN][MAXN];
int N, M;
int dx[] = {0, 0, 0, 1, -1};
int dy[] = {0, 1, -1, 0, 0};
int min_step = 1<< 30;
void print(int a[][MAXN])
{
    for(int c = 1 ;c <= M;c++){
        for(int r = 1 ;r <=N;r++)
            cout << a[c][r] <<" ";
        cout << endl;
    }
}
void change(int x, int y)
{
    for(int i = 0 ;i<5;i++)
    {
        int nx = x + dx[i] , ny = y +dy[i];
        record[nx][ny] ^=1;
    }
}

int canSolve()
{
    int step = 0;
    memcpy(record , input,  sizeof input);
    for(int r=1; r<=N;r++) if(op[1][r])  change(1,r) , step++;
    for(int c=2; c<=M;c++)
        for(int r = 1 ; r<=N;r++)
        {
            if(record[c-1][r])// 如果上面一行是脏的, 我就改变下面的行数
                op[c][r] = 1 , change(c,r),step++;
        }
  
    for(int r = 1 ; r<=N; r++)
        if (record[M][r]) return 0;
  
    return step;
}
signed main()
{
    cin.sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);

    cin >> M >> N ;
    for(int c = 1;  c<= M;c++)
        for(int r = 1 ;r<=N;r++)
            cin >> input[c][r];
  
    for(int i = 0; i<(1 << N); i++) // 枚举第一行的所有状态
    {
        memset(op , 0 , sizeof op);
        for(int r = 0 ;r < N ;r ++)
            op[1][N - r] = (i >> r & 1) ; // i的每一位依次放入op 数组

        int res = canSolve(); 
        if ( 0 < res && res < min_step )
            min_step = res ,memcpy(ans , op , sizeof ans);
    }

    if (min_step < (1<<30))
        print(ans);
    else
        cout <<"IMPOSSIBLE" << endl;
    return 0;

}


```

## 总结

状态压缩基本上就是用一个int 或者 long long 存不同的状态, 然后枚举这些状态看看最后是否符合题意.

这个题卡了我好久, 感觉话都在代码和注释里了, 本来觉着写博客我会认真写, 但是写完题感觉真的燃尽了hh

今天先这样吧, 明天还有一道题,明天再总结了, 一个月有100-120道训练量其实就不错了, 感觉还要留一点时间给科研.
