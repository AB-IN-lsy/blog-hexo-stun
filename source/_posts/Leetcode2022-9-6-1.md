---
title: 1359. 有效的快递序列数目
tags:
  - Leetcode
  - 每日一题
  - dp
categories:
  - [ACM] 
  - [2022大四上学期] 
  - [C++]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-09-06 14:26:00
---


{% note info %}
**摘要**
Title: 1359. 有效的快递序列数目
Tag: dp
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/count-all-valid-pickup-and-delivery-options/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1359. 有效的快递序列数目</font>

* ## <font size=4 face=粗体>题意</font>

  >给你 n 笔订单，每笔订单都需要快递服务。
  >请你统计所有有效的 收件/配送 序列的数目，确保第 i 个物品的配送服务 delivery(i) 总是在其收件服务 pickup(i) 之后。
  >由于答案可能很大，请返回答案对 10^9 + 7 取余的结果。

* ## <font size=4 face=粗体>思路</font>

  **状态表示**: f[i]表示考虑前i笔订单,所有的可能序列
  **集合划分**: 可以根据第i笔订单的pi和di是否挨着进行划分

  **状态计算**:
  前i - 1笔订单的序列数目为f[i - 1]
  * **当pi和di挨着**,将pi和di看成一个整体,相当于从前面2 * (i - 1)个元素中插入一个元素
    2 * (i - 1)个元素中插入一个元素总共有**2 * (i - 1) + 1**种插入方式
  * **当pi和di不挨着时**,相当于从前面2 * (i - 1)个元素中插入两个元素
    2 * (i - 1)个元素中插入两个元素总共有**C(2 * (i - 1) + 1, 2)**种插入方式

  所以 f[i] = f[i - 1] * (2 * (i - 1) + 1 + C(2 * (i - 1) + 1, 2))
  化简整理可得 f[i] = f[i - 1] * (2 * i - 1) * i

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  #include <bits/stdc++.h>
  using namespace std;

  // ---------------------
  #define N n + 100
  #define SZ(X) ((int)(X).size())
  #define int long long
  #define DEBUG(X) cout << #X << ": " << X << '\n'
  typedef pair<int, int> PII;

  // #undef N
  // const int N = 1e5 + 10;

  static int IOS = []() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
      cout.tie(nullptr);
      return 0;
  }();

  class Solution
  {
    public:
      int countOrders(int n)
      {
          vector<int> f(N);
          const int P = 1e9 + 7;
          f[1] = 1;
          for (int i = 2; i <= n; ++i)
          {
              f[i] = f[i - 1] * (2 * i - 1) * i % P;
          }
          return f[n];
      }
  };

  #undef int;

  // ---------------------
  ```