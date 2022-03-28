---
title: Nowcoder 英语作文
tags:
  - Nowcoder
  - 每日一题
  - 双指针
  - 二分
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
date: 2022-03-28 21:04:16
---


{% note info %}
**摘要**
Title: Nowcoder 英语作文
Tag: 双指针、二分
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/11223/C)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder 英语作文</font>

* ## <font size=4 face=粗体>题意</font>

  >在写英语作文的时候，两个相同单词靠的太近肯定不好。现在 ZHR 给了你一段n个单词的英文，问你有多少对相同单词中间间隔的单词数小于等于k 。

* ## <font size=4 face=粗体>思路</font>

  题目相当于问，有多少对间隔小于等于k的单词

  **二分**：每个单词维护一个vector，记录单词的下标，每次进行二分$i - k$即可
  **双指针**：每次统计此单词前面满足条件的单词有多少个，当$i > k + 1$说明超过了，对应的开头$m[a[i-k-1]]--$即可

* ## <font size=4 face=粗体>代码</font>

  **二分**
  ```cpp
  #include <algorithm>
  #include <cstring>
  #include <iostream>
  #include <unordered_map>
  #include <vector>

  using namespace std;
  const int N = 1e5 + 10;
  unordered_map<string, vector<int>> v;

  int main()
  {
      int n, k;
      cin >> n >> k;
      string s;
      long long cnt = 0, ans = 0;
      while (cin >> s)
      {
          ans += v[s].size() - (lower_bound(v[s].begin(), v[s].end(), cnt - k) - v[s].begin());
          v[s].push_back(++cnt);
      }
      cout << ans << '\n';
  }
  ```
  ****

  **双指针**
  ```cpp
  /*
  * @Author: NEFU AB-IN
  * @Date: 2021-10-25 10:13:38
  * @FilePath: \ACM\test.cpp
  * @LastEditTime: 2022-03-28 21:09:43
  */
  #include <bits/stdc++.h>
  using namespace std;
  string a[100005];
  int main()
  {
      int n, k;
      long long sum = 0;
      cin >> n >> k;
      map<string, int> m;
      for (int i = 1; i <= n; i++)
      {
          cin >> a[i];
          sum = sum + m[a[i]];
          m[a[i]]++;
          if (i > k + 1)
              m[a[i - k - 1]]--;
      }
      cout << sum << '\n';
  }
  ```