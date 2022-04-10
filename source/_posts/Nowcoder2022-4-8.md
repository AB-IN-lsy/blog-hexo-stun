---
title: Nowcoder D. 造桥
tags:
  - Nowcoder
  - dp
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
date: 2022-04-08 21:28:08
---


{% note info %}
**摘要**
Title: Nowcoder D. 造桥
Tag: dp
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/11224/D)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder D. 造桥</font>

* ## <font size=4 face=粗体>题意</font>

  >今天是愉快的周末，牛可乐和牛妹在一起玩游戏。牛妹给了牛可乐  个造桥的零件，每个零件以字符串的形式给出，每个字符串两端的字符是零件的接口，两个零件可以通过连接不同端的接口（一个零件的左端只能连接另一个零件的右端，右端则只能连接左端）得到一个更长的零件，新零件的长度是原零件的长度之和。
  >牛妹规定，零件不能翻转，且零件左边的接口只能由该零件左边的零件去连接（这意味着，应该按顺序选取零件），右端同理。
  >牛可乐想得到牛妹的赞许，因此他要想用牛妹给的零件拼接一个尽可能长的桥梁，你能帮帮他吗？

* ## <font size=4 face=粗体>思路</font>

  ![zaoqiao](https://oss.ab-in.cn/Pictures/zaoqiao.png)

* ## <font size=4 face=粗体>代码</font>

  ```python
  '''
  Author: NEFU AB-IN
  Date: 2022-04-08 21:36:35
  FilePath: \ACM\ACnowcoder\2022.4.8\d.py
  LastEditTime: 2022-04-08 21:36:36
  '''


  def ord1(x):
      return ord(x) - ord('a')


  N = int(2e5 + 10)
  for _ in range(int(input())):
      n = int(input())
      dp = [0] * N
      for i in range(n):
          s = input()
          dp[ord1(s[-1])] = max(dp[ord1(s[-1])], dp[ord1(s[0])] + len(s))
      ans = 0
      for i in range(26):
          ans = max(ans, dp[i])
      print(ans)

  ```