---
title: Nowcoder E. 捡贝壳
tags:
  - Nowcoder
  - 二分
  - 约数
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
date: 2022-05-09 20:52:00
---


{% note info %}
**摘要**
Title: Nowcoder E. 捡贝壳
Tag: 二分、约数
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/E)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder E. 捡贝壳</font>

* ## <font size=4 face=粗体>题意</font>

  > 见原题

* ## <font size=4 face=粗体>思路</font>

  对每个数进行因子分解，每个因子后面push_back含有该因子数的下标（从小到大），对其进行二分查找即可

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  /*
  * @Author: NEFU AB-IN
  * @Date: 2022-05-09 15:38:38
  * @FilePath: \ACM\ACnowcoder\34349\e.cpp
  * @LastEditTime: 2022-05-09 20:51:24
  */
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define SZ(X) ((int)(X).size())
  #define ALL(X) (X).begin(), (X).end()
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;

  const int INF = 0x3f3f3f3f;
  const int N = 1e5 + 10;
  int n, q;

  signed main()
  {
      IOS;
      cin >> n >> q;
      vector<int> a(n + 1);
      for (int i = 1; i <= n; ++i)
          cin >> a[i];

      vector<int> g[N];

      auto get = [&](int id, int x) {
          for (int i = 1; i <= x / i; ++i)
          {
              if (x % i == 0)
              {
                  g[i].push_back(id);
                  if (i != x / i)
                      g[x / i].push_back(id);
              }
          }
      };

      for (int i = 1; i <= n; ++i)
      {
          get(i, a[i]);
      }

      while (q--)
      {
          int l, r, x;
          cin >> l >> r >> x;
          cout << upper_bound(ALL(g[x]), r) - lower_bound(ALL(g[x]), l) << '\n';
      }

      return 0;
  }
  ```