---
title: 1371. 每个元音包含偶数次的最长子字符串
tags:
  - Leetcode
  - 每日一题
  - 前缀和
  - 状态压缩
  - 哈希表
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
date: 2022-09-06 19:52:49
---


{% note info %}
**摘要**
Title: 1371. 每个元音包含偶数次的最长子字符串
Tag: 前缀和、状态压缩、哈希表
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/find-the-longest-substring-containing-vowels-in-even-counts/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1371. 每个元音包含偶数次的最长子字符串</font>

* ## <font size=4 face=粗体>题意</font>

  >给你一个字符串 s ，请你返回满足以下条件的最长子字符串的长度：每个元音字母，即 'a'，'e'，'i'，'o'，'u' ，在子字符串中都恰好出现了偶数次。

* ## <font size=4 face=粗体>思路</font>

  * 遇到奇偶个数校验，想到：**XOR**
  * 遇到有限的参数（小于20个）表状态， 想到：**状态压缩**
  * 遇到求最长的连续子串使得和为k想到：**前缀和 + 哈希表**记录第一次出现某一状态的位置

  思路
  * 利用**异或**，将奇偶型转换为01问题，奇变偶，偶变奇，就是将当前状态异或1即可
  * 利用**状态压缩**，将五个状态压缩成一个二进制表示，如01010，再转换为十进制存起来，这样就可以针对某一位进行异或
  * 利用**前缀和**去求某一区间的状态，也就是当s[i]和s[j]状态相同时，s[j + 1, i]就是符合条件的
  * 利用**哈希表**去求第一次某状态出现的下标

  此题非常经典，具体细节见代码注释
* ## <font size=4 face=粗体>代码</font>

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
      int findTheLongestSubstring(string s)
      {
          vector<int> st(32, -INT_MAX);
          // 一共 2^5 = 32种状态，初始化为负无穷，值为该状态最早的下标
          // 二进制 00001 代表 1，代表u为奇数，其他为偶数
          st[0] = -1; // 记录该下标的前一个，因为要进行前缀和操作
          string p = "aeiou";
          int state = 0; // 一开始都是偶数，即 00000
          int ans = 0;
          for (int i = 0; i < SZ(s); ++i)
          {
              int k = p.find(s[i]);
              if (k != -1)
                  state ^= (1 << k); // state 的第k位异或1，某一元音的奇偶性就变了
              if (st[state] == -INT_MAX)
                  // 说明还没更新过最小下标
                  st[state] = i;
              else
                  ans = max(ans, i - st[state]);
              // [j + 1, i] 即 i - (j + 1) + 1 即 i - j
          }
          return ans;
      }
  };

  #undef int
  // ---------------------
  ```