---
title: Nowcoder H. 有多短
tags:
  - Nowcoder
  - 树的直径
  - 思维
  - 贪心
categories:
  - [ACM]
  - [2022大三下学期]
  - [C++]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-05-09 22:46:55
---


{% note info %}
**摘要**
Title: Nowcoder H. 有多短
Tag: 树的直径、思维、贪心
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/H)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder H. 有多短</font>

* ## <font size=4 face=粗体>题意</font>

  >给定一棵n（2<=n<=100000,n∈Z+）个点的树（保证树连通），将k（0<=k<=1000000000,k∈Z）分配到各个边的权值上，使得每条边权值为A[i]（0<=A[i]<=k,A[i] ∈ R）。现求分配权值后树的直径的最小值。
  >树的直径：树上最远的两点的路径权值和。

* ## <font size=4 face=粗体>思路</font>

  **树的直径一定是两个叶子之间的路径** (叶子是树中度数为$1$的点)

  **贪心策略**：为了使得直径最小，最优解是将$k$**均摊给与叶子相连的边上**,其他边全部赋值为$0$
  （因为树的直径必走两次叶子与其他节点连的边，那么其余类型的边全为0是最优的）

  设度数为$1$的点有$cnt$个,那么答案为$2*k/cnt$,乘2是因为直径会经过两个被赋值的边


* ## <font size=4 face=粗体>代码</font>

  ```cpp
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define SZ(X) ((int)(X).size())
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;

  const int INF = 0x3f3f3f3f;
  const int N = 1e6 + 10;

  signed main()
  {
      IOS;
      int n, k;
      cin >> n >> k;
      vector<int> deg(n + 1);
      for (int i = 1; i < n; ++i)
      {
          int u, v;
          cin >> u >> v;
          deg[u]++;
          deg[v]++;
      }

      int cnt = count(deg.begin() + 1, deg.end(), 1);

      printf("%.6lf", 2.0 * k / cnt);
      return 0;
  }
  ```