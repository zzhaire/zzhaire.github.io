---
abbrlink: ''
author: null
categories:
- - acmer之路
date: '2025-10-11T10:08:23.965692+08:00'
excerpt: pots  两个水壶倒水, 得到目标容积, bfs 搜索题
tags:
- bfs
title: '刷题 :  pots'
updated: '2025-10-11T10:12:32.387+08:00'
---
## pots

> 题目链接 :  https://vjudge.net/problem/POJ-3414

## 题目描述

You are given two pots, having the volume of **A** and **B** liters respectively. The following operations can be performed:

1. FILL(i)    fill the pot **i** (1 ≤ **i** ≤ 2) from the tap;
2. DROP(i)   empty the pot **i** to the drain;
3. POUR(i,j)  pour from pot **i** to pot **j**; after this operation either the pot **j** is full (and there may be some water left in the pot **i**), or the pot **i** is empty (and all its contents have been moved to the pot **j**).

Write a program to find the shortest possible sequence of these operations that will yield exactly **C** liters of water in one of the pots.

### Input

On the first and only line are the numbers **A**, **B**, and **C**. These are all integers in the range from 1 to 100 and **C**≤max(**A**,**B**).

### Output

The first line of the output must contain the length of the sequence of operations **K**. The following **K** lines must each describe one operation. If there are several sequences of minimal length, output any one of them. If the desired result can’t be achieved, the first and only line of the file must contain the word ‘**impossible**’.

## sample


| Input | Output                                                                    |
| ----- | ------------------------------------------------------------------------- |
| 3 5 4 | 6<br>FILL(2)<br>POUR(2,1)<br>DROP(1)<br>POUR(2,1)<br>FILL(2)<br>POUR(2,1) |

## 题目思路

### 1.状态表示与映射

为了将二维状态$(n_A,n_B)$存储在一个一维数组中进行查重( vis 数组),我们使用一个唯一的整数 ID 来表
示状态。
· 状态 ID: $ID=n_A\times100+n_B$
· 由于$A,B\leq100$,我们使用100作为乘数可以保证$n_{A}$和$n_{B}$能被唯一地解析出来。
· 状态逆映射( convert 函数):

$$
n_A=\lfloor\frac{ID}{100}\rfloor,\quad n_B=ID\quad(\mathrm{mod~}100)
$$

### 2. 状态转移（操作）

共有 6 种操作，每种操作都定义在全局的 op 函数中，它修改全局的 pots 状态并返回新的 ID。


| 操作 ID | 操作名称   | 描述                                  |
| ------- | ---------- | ------------------------------------- |
| 1       | FILL(1)    | 将壶 1 灌满 (n_A = A)                 |
| 2       | FILL(2)    | 将壶 2 灌满 (n_B = B)                 |
| 3       | DROP(1)    | 将壶 1 倒空 (n_A = 0)                 |
| 4       | DROP(2)    | 将壶 2 倒空 (n_B = 0)                 |
| 5       | POUR(1, 2) | 从壶 1 倒入壶 2，直到壶 2 满或壶 1 空 |
| 6       | POUR(2, 1) | 从壶 2 倒入壶 1，直到壶 1 满或壶 2 空 |

关键的编程技巧：在 BFS 循环中，每次枚举完一个操作后，必须调用 convert(now) 恢复全局 pots 的水量，以确保下一个操作是基于原始状态 now 进行的，而不是基于上一个操作修改后的状态。

### 3. BFS 过程

1. **初始化：** 将起始状态 (0,0) (ID 为 0) 入队，标记 `vis[0] = 1`。
2. **记录路径：** 使用 `record` 数组存储到达每个状态所需的步数、父节点 ID 和执行的操作字符串。
3. **循环：**
   - 取出队首状态 `now`。
   - 使用 `convert(now)` **恢复**全局 `pots` 的水量。
   - **检查目标：** 若 `pots[1].n == C` 或 `pots[2].n == C`，则找到最短路径，进入回溯。
   - **扩展状态：** 遍历 6 种操作 i：
     - 调用 `op(i)` 获得新状态 `nstate`。
     - 若 `nstate` 未被访问，则标记 `vis[nstate] = 1`，记录路径信息，并将其入队。
     - 调用 `convert(now)` **恢复**全局 `pots` 状态，以便下一个操作从 `now` 开始。
4. **失败：** 若队列为空仍未找到目标，则输出 `impossible`。

### 4. 路径回溯与输出

找到目标状态 `now` 后，我们通过 `record[now].father` 沿着路径逆向回溯，将操作字符串推入栈 `ans`。

由于我们在回溯时会记录起始状态 ID 0 对应的空操作 `""`，因此在输出时，需要**丢弃**栈中的第一个（即起始状态的）空操作，并确保格式正确。

## AC代码

```cpp
#include <iostream>
#include <queue>
#include <string>
#include<stack>
using namespace std;
int A, B, C;
int vis[10010];
struct pot
{
    int n, v;
    void set(int i) { v = i, n = 0; }
} pots[3];
void FILL(int i)
{
    pots[i].n = pots[i].v;
}
void DROP(int i)
{
    pots[i].n = 0;
}
void POUR(int i, int j){
    int left = pots[j].v - pots[j].n;
    if (left > pots[i].n)
        left = pots[i].n;
    pots[i].n -= left; pots[j].n += left;
}
struct step{
    int id, step, father;
    string op;
} record[10010];
int state()
{
    return pots[1].n * 100 + pots[2].n;
}
void convert(int id)
{
    pots[1].n = id / 100;
    pots[2].n = id % 100;
}
bool check(int id)
{
    convert(id);
    if (pots[1].n == C)return 1;
    if (pots[2].n == C)return 1;
    return 0;
}
int op(int id)
{
    switch (id)
    {
    case 1:FILL(1);break;
    case 2:FILL(2);break;
    case 3:DROP(1);break;
    case 4:DROP(2);break;
    case 5:POUR(1, 2);break;
    case 6:POUR(2, 1);break;
    }
    return state();
}
const string opstring[] = {
    "",
    "FILL(1)",
    "FILL(2)",
    "DROP(1)",
    "DROP(2)",
    "POUR(1,2)",
    "POUR(2,1)",
};
stack<string> ans;
int BFS(){
    queue<step> q;
    q.push({0, 0, -1, ""});
    record[0] = {0, 0, -1, ""};
    vis[0] = 1;
    while (q.size())
    {
        step t = q.front();
        q.pop();
        int now = t.id;convert(t.id); // 由于之前恢复了状态枚举, 所以到这一步要重新根据 id 改回来
        if (check(now))
        {
            for(int i = now ; ~i ; i = record[i].father)
                ans.push(record[i].op);
            return t.step;
        }
        // enum states
        for (int i = 1; i <= 6; i++)
        {
            int nstate = op(i);
            if (!vis[nstate])
            {
                vis[nstate] = 1;
                q.push({nstate, t.step + 1, now, opstring[i]});
                record[nstate] = {nstate, t.step + 1, now, opstring[i]};
            }
            convert(now); // 每次操作后恢复状态继续枚举
        }
    }
    return -1;
}
signed main()
{
    cin >> A >> B >> C;
    pots[1].set(A);
    pots[2].set(B);
    int res = BFS();
    if (res == -1)
    {
        cout << "impossible" << endl;
        return 0;
    }
    cout << res << endl;
    ans.pop();
    while (ans.size())
    {
        cout << ans.top() << endl;
        ans.pop();
    }
}

```
