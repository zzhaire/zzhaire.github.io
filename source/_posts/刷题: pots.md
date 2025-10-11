---
abbrlink: ''
author: null
categories:
- - acmer之路
date: '2025-10-11T10:08:23.965692+08:00'
excerpt: pots  题目链接 : https://vjudge.net/problem/POJ-3414  ...
tags:
- bfs
title: '刷题 :  pots'
updated: '2025-10-11T10:12:32.387+08:00'
---
## pots

> 题目链接 : https://vjudge.net/problem/POJ-3414

## 题目描述


You are given two pots, having the volume of **A** and **B** liters respectively. The following operations can be performed:

1. FILL(i)        fill the pot **i** (1 ≤ **i **≤ 2) from the tap;
2. DROP(i)      empty the pot **i** to the drain;
3. POUR(i,j)    pour from pot **i** to pot **j**; after this operation either the pot **j** is full (and there may be some water left in the pot **i**), or the pot **i** is empty (and all its contents have been moved to the pot **j**).

Write a program to find the shortest possible sequence of these operations that will yield exactly **C** liters of water in one of the pots.

### Input

On the first and only line are the numbers **A**, **B**, and **C**. These are all integers in the range from 1 to 100 and **C**≤max(**A**,**B**).

### Output

The first line of the output must contain the length of the sequence of operations **K**. The following **K** lines must each describe one operation. If there are several sequences of minimal length, output any one of them. If the desired result can’t be achieved, the first and only line of the file must contain the word ‘**impossible**’.
