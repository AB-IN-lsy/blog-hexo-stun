---
title: Nowcoder G 分割
tags:
  - Nowcoder
  - 规律
  - 数学
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
date: 2022-05-09 21:48:54
---


{% note info %}
**摘要**
Title: Nowcoder G 分割
Tag: 数学、规律
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/G)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder G 分割</font>

* ## <font size=4 face=粗体>题意</font>

  >在一个二维平面，
  >有n条平行于y轴的直线, 他们的x坐标是x[i]，
  >m条平行于x轴的直线y[i]，他们的y坐标是y[i].
  >求出这些直线所有可能形成矩形的总面积对1000000007取模的值。
  >保证所有直线不完全重叠。

* ## <font size=4 face=粗体>思路</font>

  题目是要任取两条横线,两条竖线,将所有可能的方案组成的矩形面积相加.

  容易发现**横线的选择和竖线的选择是相互独立的**,
  因此我们只需要计算出选择两条横线能组成的所有矩形边长的和,
  同时计算出选择两条竖线能组成的所有矩形变成的和,
  两者相乘就是答案.

  现在问题变为如何计算所有能组成的边长的和.

  对于x[i]
  对答案的贡献为`x[i]-x[0],x[i]-x[1],...x[i]-x[i-1]`,这些数的和.
  合并一下就是`x[i]*i-sum(x[0]+x[1]...x[i-1])`,
  维护一个前缀sum就可以O(n)计算了.


* ## <font size=4 face=粗体>代码</font>

  ps: **一定要注意，当vector下标从1开始时，就不能直接从a.begin()开始了，得+1**
  ```cpp
  #include <bits/stdc++.h>
  #define int long long
  #define ALL(X) (X).begin(), (X).end()
  using namespace std;

  const int MOD = 1000000007;
  signed main()
  {
      int n, m;
      cin >> n >> m;
      vector<int> x(n);
      for (int i = 0; i < n; ++i)
          cin >> x[i];

      vector<int> y(m);
      for (int i = 0; i < m; ++i)
          cin >> y[i];

      sort(ALL(x));
      sort(ALL(y));

      int ansx = 0, ansy = 0, sum = 0;
      for (int i = 0; i < n; ++i)
      {
          ansx = (ansx + i * x[i] - sum) % MOD;
          sum = (sum + x[i]) % MOD;
      }
      sum = 0;
      for (int i = 0; i < m; ++i)
      {
          ansy = (ansy + i * y[i] - sum) % MOD;
          sum = (sum + y[i]) % MOD;
      }
      cout << ansx * ansy % MOD;

      return 0;
  }
  ```