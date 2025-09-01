---
abbrlink: ''
author: zzhaire
categories:
- - acmer之路
date: '2025-09-01T22:24:08.269743+08:00'
tags:
- bfs
- 搜索
title: Dungeon Master
updated: '2025-09-01T22:24:08.771+08:00'
---
## 题目链接

> https://vjudge.net/problem/POJ-2251

## 题目描述

You are trapped in a 3D dungeon and need to find the quickest way out! The dungeon is composed of unit cubes which may or may not be filled with rock. It takes one minute to move one unit north, south, east, west, up or down. You cannot move diagonally and the maze is surrounded by solid rock on all sides.

Is an escape possible? If yes, how long will it take?

### Input

The input consists of a number of dungeons. Each dungeon description starts with a line containing three integers L, R and C (all limited to 30 in size).
L is the number of levels making up the dungeon.
R and C are the number of rows and columns making up the plan of each level.
Then there will follow L blocks of R lines each containing C characters. Each character describes one cell of the dungeon. A cell full of rock is indicated by a '#' and empty cells are represented by a '.'. Your starting position is indicated by 'S' and the exit by the letter 'E'. There's a single blank line after each level. Input is terminated by three zeroes for L, R and C.

### Output

Each maze generates one line of output. If it is possible to reach the exit, print a line of the form

> Escaped in x minute(s).

where x is replaced by the shortest time it takes to escape.
If it is not possible to escape, print the line

> Trapped!

## 思路

中文意思大概就是走迷宫, 3D 迷宫, 很经典的bfs 题目, 没有什么难度

## AC 代码

```cpp

#include <iostream>
#include <queue>
#include <cstring>
using namespace std;
const int N = 31;
char g[N][N][N];
int vis[N][N][N];
int dx[] = {0, 0, 0, 0, 1, -1};
int dy[] = {1, -1, 0, 0, 0, 0};
int dz[] = {0, 0, 1, -1, 0, 0};
int L, R, C;
int ans;
int sl, sr, sc;
int el, er, ec;
struct coord {
    int x, y, z, s;
};
int bfs()
{
    queue<coord> q;
    coord c;
    c.x = sl;
    c.y = sr;
    c.z = sc;
    c.s = 0;
    q.push({sl,sr,sc,0});
    q.push(c);
    vis[sl][sr][sc] = 1;
    while (q.size())
    {
        coord t = q.front();
        q.pop();
        int dl, dr, dc;
        for (int i = 0; i < 6; i++)
        {
            dl = t.x + dx[i];
            dr = t.y + dy[i];
            dc = t.z + dz[i];
            if (vis[dl][dr][dc])
                continue;
            if (g[dl][dr][dc] == '#')
                continue;
            if (g[dl][dr][dc] == 'E')
                return t.s + 1;
            if (dl <= 0 || dl > L)
                continue;
            if (dr <= 0 || dr > R)
                continue;
            if (dc <= 0 || dc > C)
                continue;
            vis[dl][dr][dc] = 1;
            // cout << dl <<" " << dr <<" " << dc <<" " << t[3]<< endl;
            coord next;
            next.x = dl;
            next.y = dr;
            next.z = dc;
            next.s = t.s + 1;
            q.push(next);
        }
    }
    return 0;
}
signed main()
{
    while (cin >> L >> R >> C && L && R && C)
    {
        for (int l = 1; l <= L; l++)
        {
            for (int r = 1; r <= R; r++)
            {
                for (int c = 1; c <= C; c++)
                {
                    char &x = g[l][r][c];
                    cin >> x;
                    if (x == 'S')
                        sl = l, sr = r, sc = c;
                    if (x == 'E')
                        el = l, er = r, ec = c;
                }
            }
        }
        memset(vis, 0 ,sizeof vis);
        // cout <<" debug " << endl;
        ans = bfs();
        // cout << ans << endl;

        if (ans)
            cout << "Escaped in " << ans << " minute(s)." << endl;
        else
            cout << "Trapped!" << endl;
    }
}
```

## 吐槽一句

这个oj 有点老了, auto [x , y] : 这种都识别不了, 有点烦人, 而且也不能使用万能头, 不过也好, 帮我培养一下代码习惯, 刷题的第二题, 加油
