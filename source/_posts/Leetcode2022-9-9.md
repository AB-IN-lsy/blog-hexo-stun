---
title: 1387. 将整数按权重排序
tags:
  - Acwing
  - 每日一题
  - DFS
  - 剪枝
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
date: 2022-09-09 13:48:10
---


{% note info %}
**摘要**
Title: 1387. 将整数按权重排序
Tag: DFS、剪枝
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/sort-integers-by-the-power-value/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1387. 将整数按权重排序</font>

* ## <font size=4 face=粗体>题意</font>

  >我们将整数 x 的 权重 定义为按照下述规则将 x 变成 1 所需要的步数：
  >如果 x 是偶数，那么 x = x / 2
  >如果 x 是奇数，那么 x = 3 * x + 1
  >比方说，x=3 的权重为 7 。因为 3 需要 7 步变成 1 （3 --> 10 --> 5 --> 16 --> 8 --> 4 --> 2 --> 1）。
  >给你三个整数 lo， hi 和 k 。你的任务是将区间 [lo, hi] 之间的整数按照它们的权重 升序排序 ，如果大于等于 2 个整数有 相同 的权重，那么按照数字自身的数值 升序排序 。
  >请你返回区间 [lo, hi] 之间的整数按权重排序后的第 k 个数。
  >注意，题目保证对于任意整数 x （lo <= x <= hi） ，它变成 1 所需要的步数是一个 32 位有符号整数。

* ## <font size=4 face=粗体>思路</font>

  * 正常DFS，之后排序即可
  * 优化:
    * 可以观察到奇数x需变成3x+1，也就是肯定是偶数，那么偶数肯定就需要除以2，那么就可以融合成一步完成
    * 另外，当生成了某数的权重后，可以利用之前的结果，也就是进行记忆化搜索
    * 不懂为什么优化了之后慢了。。

* ## <font size=4 face=粗体>代码</font>

  无剪枝
  ```cpp
  // ---------------------
  #define N n + 100
  #define int long long
  #define SZ(X) ((int)(X).size())
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
      int dfs(int x)
      {
          if (x == 1)
              return 0;
          if (x & 1)
              return 1 + dfs(3 * x + 1);
          else
              return 1 + dfs(x / 2);
      }

      int getKth(int lo, int hi, int k)
      {
          vector<PII> ans;
          for (int i = lo; i <= hi; ++i)
          {
              ans.push_back({dfs(i), i});
          }
          sort(ans.begin(), ans.end());
          return ans[k - 1].second;
      }
  };

  #undef int
  // ---------------------
  ```

  ****
  优化

  ```cpp
  // ---------------------
  #define N n + 100
  #define int long long
  #define SZ(X) ((int)(X).size())
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
      unordered_map<int, int> mp;
      int dfs(int x)
      {
          if(mp.count(x)) return mp[x];
          if (x == 1)
              return 0;
          if (x & 1)
              return mp[x] = 2 + dfs((3 * x + 1) / 2);
          else
              return mp[x] = 1 + dfs(x / 2);
      }

      int getKth(int lo, int hi, int k)
      {
          vector<PII> ans;
          for (int i = lo; i <= hi; ++i)
          {
              ans.push_back({dfs(i), i});
          }
          sort(ans.begin(), ans.end());
          return ans[k - 1].second;
      }
  };

  #undef int
  // ---------------------
```