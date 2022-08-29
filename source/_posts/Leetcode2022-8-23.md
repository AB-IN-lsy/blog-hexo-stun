---
title: 768. 最多能完成排序的块 II
tags:
  - Leetcode
  - 每日一题
  - 哈希表
  - 单调栈
categories:
  - [ACM] 
  - [2022大三暑假] 
  - [C++]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-08-23 09:17:26
---


{% note info %}
**摘要**
Title: 768. 最多能完成排序的块 II
Tag: 哈希表，单调栈
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/max-chunks-to-make-sorted-ii/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>768. 最多能完成排序的块 II</font>

* ## <font size=4 face=粗体>题意</font>

  >arr是一个可能包含重复元素的整数数组，我们将这个数组分割成几个“块”，并将这些块分别进行排序。之后再连接起来，使得连接的结果和按升序排序后的原数组相同。
  >我们最多能将数组分成多少块？

* ## <font size=4 face=粗体>思路</font>

  见官方题解，两种思路：
  * 单调栈
    * 遵循，**左边的区间的所有数字均小于等于右边的区间的所有数字**
  * 哈希表
    * 部分区间排序后和排序前频次相同，就是一个可划分的区间

* ## <font size=4 face=粗体>代码</font>

  单调栈
  ```cpp
  static int x = []() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
      cout.tie(nullptr);
      return 0;
  }();

  #define SZ(X) ((int)(X).size())

  class Solution
  {
    public:
      int maxChunksToSorted(vector<int> &arr)
      {
          stack<int> s;
          for (auto i : arr)
          {
              if (!SZ(s) || i >= s.top())
                  s.push(i);
              else
              {
                  int mx = s.top();
                  s.pop();
                  while (SZ(s) && s.top() > i)
                      s.pop();
                  s.push(mx);
              }
          }
          return SZ(s);
      }
  };
  ```

  哈希表
  ```cpp
  class Solution {
  public:
      int maxChunksToSorted(vector<int>& arr) {
          unordered_map<int, int> cnt; // 用于计数
          int res = 0;
          vector<int> Sort = arr;
          sort(Sort.begin(), Sort.end()); // 排序
          // 遍历每个数字
          for (int i = 0; i < arr.size(); i ++ )
          {
              int a = arr[i], b = Sort[i];
              // 按上述操作执行
              cnt[a] ++ ;
              if (!cnt[a]) cnt.erase(a); // 如果这个数字没有了则在计数数组中删除它
              cnt[b] -- ;
              if (!cnt[b]) cnt.erase(b); // 同上
              if (!cnt.size()) res ++ ; // 词频相同，答案加一
          }
          return res;
      }
  };
  ```