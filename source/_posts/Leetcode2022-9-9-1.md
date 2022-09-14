---
title: 1386. 安排电影院座位
tags:
  - Leetcode
  - 每日一题
  - bitset
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
date: 2022-09-09 16:16:10
---


{% note info %}
**摘要**
Title: 1386. 安排电影院座位
Tag: bitset
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/cinema-seat-allocation/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1386. 安排电影院座位</font>

* ## <font size=4 face=粗体>题意</font>

  >如上图所示，电影院的观影厅中有 n 行座位，行编号从 1 到 n ，且每一行内总共有 10 个座位，列编号从 1 到 10 。
  >给你数组 reservedSeats ，包含所有已经被预约了的座位。比如说，researvedSeats[i]=[3,8] ，它表示第 3 行第 8 个座位被预约了。
  >请你返回 最多能安排多少个 4 人家庭 。4 人家庭要占据 同一行内连续 的 4 个座位。隔着过道的座位（比方说 [3,3] 和 [3,4]）不是连续的座位，但是如果你可以将 4 人家庭拆成过道两边各坐 2 人，这样子是允许的。


* ## <font size=4 face=粗体>思路</font>

  由于排的数量很多，所以枚举每排的话是不现实的
  所以我们可以采用**哈希表**，来记录2~9有座位被占了的排（因为占1或10，和没占没什么区别，都是能做俩）
  其次，可以用**二进制串**来记录这排的位置情况，1代表占了（可以采用bitset，也可以采用int）
  最后取反一下，每行的状态，和left, mid, right进行&操作，如果&之后还是原值的话，那么说明可以放一个

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  /*
  * @Author: NEFU AB-IN
  * @Date: 2022-09-09 14:13:18
  * @FilePath: \LeetCode\1386\1386.cpp
  * @LastEditTime: 2022-09-09 16:15:18
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

  static int IOS = []() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
      cout.tie(nullptr);
      return 0;
  }();

  class Solution
  {
    public:
      int maxNumberOfFamilies(int n, vector<vector<int>> &reservedSeats)
      {
          bitset<11> left{0b111100000}, mid{0b1111000}, right{0b11110};

          // 2~5 4~7 6~9
          unordered_map<int, bitset<11>> mp;
          for (auto v : reservedSeats)
          {
              int h = v[0], l = v[1];
              if (l >= 2 && l <= 9)
              {
                  mp[h].set(10 - l);
              }
          }
          int ans = (n - SZ(mp)) * 2;
          for (auto [h, b] : mp)
          {
              b = ~b;
              // DEBUG(right);
              if (((b & left) == left) || ((b & right) == right) || ((b & mid) == mid))
                  ans++;
          }
          return ans;
      }
  };

  // ---------------------

  // signed main()
  // {
  //     Solution solution;
  //     vector<vector<int>> a = {{1, 2}, {1, 3}, {1, 8}, {2, 6}, {3, 1}, {3, 10}};
  //     cout << solution.maxNumberOfFamilies(3, a);
  //     return 0;
  // }
  ```