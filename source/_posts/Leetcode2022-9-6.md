---
title: 1345. 跳跃游戏 IV 
tags:
  - Leetcode
  - 每日一题
  - 哈希
  - BFS
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
date: 2022-09-06 14:07:40
---


{% note info %}
**摘要**
Title: 1345. 跳跃游戏 IV 
Tag: 哈希、BFS
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/jump-game-iv/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1345. 跳跃游戏 IV </font>

* ## <font size=4 face=粗体>题意</font>

  > 略

* ## <font size=4 face=粗体>思路</font>

  先用哈希表将每个相同元素的位置记下来，每个形成一个链表，再进行BFS，入队的话，就让前一个、后一个、链表的元素入队即可
  其中减少复杂度的操作，就是当遍历完自己的链表后，将其从哈希表中删去，因为再遍历肯定是不优的

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  /*
  * @Author: NEFU AB-IN
  * @Date: 2022-09-05 21:10:01
  * @FilePath: \LeetCode\1345\1345.cpp
  * @LastEditTime: 2022-09-06 14:06:02
  */
  #include <bits/stdc++.h>
  using namespace std;

  // ---------------------
  #define N n + 100
  #define SZ(X) ((int)(X).size())
  #define DEBUG(X) cout << #X << ": " << X << '\n'
  typedef pair<int, int> PII;

  // #undef N
  // const int N = 1e5 + 10;

  // #undef int;

  static int IOS = []() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
      cout.tie(nullptr);
      return 0;
  }();

  class Solution
  {
    public:
      int minJumps(vector<int> &arr)
      {
          int n = SZ(arr);
          queue<PII> q;
          unordered_map<int, vector<int>> g;
          for (int i = 0; i < n; ++i)
          {
              g[arr[i]].push_back(i);
          }

          vector<int> st(n);
          st[0] = 1;
          q.push({0, 0});

          while (SZ(q))
          {
              auto t = q.front();
              q.pop();

              int id = t.first, cnt = t.second;

              if (id == n - 1)
              {
                  return cnt;
              }
              if (g.count(arr[id]))
              {
                  for (auto v : g[arr[id]])
                  {
                      if (!st[v])
                          q.push({v, cnt + 1}), st[v] = 1;
                  }
                  g.erase(arr[id]); // 遍历完一遍了，直接就可以删掉了
              }
              if (id >= 1 && !st[id - 1])
                  q.push({id - 1, cnt + 1}), st[id - 1] = 1;
              if (id <= n - 1 && !st[id + 1])
                  q.push({id + 1, cnt + 1}), st[id + 1] = 1;
          }
          return 0;
      }
  };

  // ---------------------

  signed main()
  {
      Solution solution;
      return 0;
  }
  ```