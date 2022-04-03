---
title: Nowcoder B. 抓球
tags:
  - Acwing
  - 每日一题
  - 组合数
categories:
  - [ACM]
  - [2022大三下学期]
  - [Python]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-04-03 17:12:45
---


{% note info %}
**摘要**
Title: Nowcoder B. 抓球
Tag: 组合数
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/30825/B)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder B. 抓球</font>

* ## <font size=4 face=粗体>题意</font>

  >一个箱子里有n个黑球，m个白球，小王想要连续q次从箱子里随机的取出k个球（每次取出k个后立即放回），连续q次取球k个都为黑球的概率是多少，结果对1e9+7取模。

* ## <font size=4 face=粗体>思路</font>

  推出式子为
  $$
  \frac{C_{n}^{k}}{C_{n + m}^{k}}
  $$

  ps: 关于组合数的计算
    * 一定要边算边取模
    * 算出一次的概率，再算多次的

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  /*
  * @Author: NEFU AB-IN
  * @Date: 2022-04-03 15:12:00
  * @FilePath: \ACM\ACnowcoder\2022.4.3\b.cpp
  * @LastEditTime: 2022-04-03 15:59:53
  */
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define MP make_pair
  #define SZ(X) ((int)(X).size())
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;
  const int MOD = 1e9 + 7;

  const int N = 5e6 + 10;
  int fact[N], infact[N];

  int qp(int a, int b, int p)
  {
      int res = 1;
      while (b)
      {
          if (b & 1)
              res = res * a % p;
          b >>= 1;
          a = a * a % p;
      }
      return res;
  }

  signed main()
  {
      int t;
      scanf("%lld", &t);
      fact[0] = infact[0] = 1;
      for (int i = 1; i < N; ++i)
      {
          fact[i] = fact[i - 1] * i % MOD;
          infact[i] = infact[i - 1] * qp(i, MOD - 2, MOD) % MOD;
      }
      while (t--)
      {
          int n, m, k, q;
          scanf("%lld%lld%lld%lld", &n, &m, &k, &q);
          if (k > n)
          {
              printf("0\n");
              continue;
          }
          int t = fact[n] * infact[m + n] % MOD * fact[m + n - k] % MOD * infact[n - k] % MOD;
          printf("%lld\n", qp(t, q, MOD) % MOD);
      }
      return 0;
  }
  ```