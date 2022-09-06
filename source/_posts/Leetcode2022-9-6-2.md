---
title: 1360. 日期之间隔几天
tags:
  - Leetcode
  - 每日一题
  - 日期问题
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
date: 2022-09-06 16:15:45
---


{% note info %}
**摘要**
Title: 1360. 日期之间隔几天
Tag: 日期问题
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/number-of-days-between-two-dates/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1360. 日期之间隔几天</font>

* ## <font size=4 face=粗体>题意</font>

  >请你编写一个程序来计算两个日期之间隔了多少天。
  >日期以字符串形式给出，格式为 YYYY-MM-DD，如示例所示。

* ## <font size=4 face=粗体>思路</font>

  思路就是，写出一个函数，功能是**求出此时这个日期在这一年是第几天**
  
  然后
  * 求第一个结果，是用a年的天数，减去a这个日期在a这一年是第几天
  * 求第二个结果，这两个年中隔了多少年
  * 求第三个结果，b这个日期在b这一年是第几天

  三个相加就是答案
  细节：
  * 闰年和平年
  * 若是同一年的话需要取余

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
      int daysBetweenDates(string date1, string date2)
      {
          if (date1 > date2)
              swap(date1, date2);
          int y1, m1, d1, y2, m2, d2;

          sscanf(date1.c_str(), "%lld-%lld-%lld", &y1, &m1, &d1);
          sscanf(date2.c_str(), "%lld-%lld-%lld", &y2, &m2, &d2);

          vector<int> months = {0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31};

          auto check = [&](int y) { return y % 400 == 0 || (y % 100 && y % 4 == 0); };

          auto f = [&](vector<int> months, int y, int m, int d) {
              if (check(y))
                  months[2]++;
              int x = d;
              for (int i = 1; i <= m - 1; ++i)
                  x += months[i];
              return x;
          };

          int x1 = 365 + check(y1) - f(months, y1, m1, d1);
          int x2 = f(months, y2, m2, d2);

          int x3 = 0;
          for (int i = y1 + 1; i <= y2 - 1; ++i)
          {
              x3 += (365 + check(i));
          }
          int ans = x1 + x2 + x3;
          if (y1 == y2)
              ans %= (365 + check(y1));
          return ans;
      }
  };

  #undef int;
  // ---------------------
  ```