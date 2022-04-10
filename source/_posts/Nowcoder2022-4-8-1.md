---
title: Nowcoder C. 小猫排队
tags:
  - Nowcoder
  - 模拟
  - 栈
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
date: 2022-04-08 21:34:23
---


{% note info %}
**摘要**
Title: Nowcoder C. 小猫排队
Tag: 模拟、栈
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/11224/C)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder C. 小猫排队</font>

* ## <font size=4 face=粗体>题意</font>

  >世界上最苦恼的事情莫过于排队了，特别是排在你前面的猫比你可爱的时候。----《论猫的自我修养》
  >小猫啾啾现在就很苦恼，它排在队伍的末尾处等着买酱油，前面还有足足  只猫咪。但幸运的是小猫啾啾会一种魔法：它可以和前面距离它最近且比它可爱（可爱值大于啾啾）的小猫交换位置（被交换的小猫会被传送到啾啾之前的位置）。
  >已知啾啾每一分钟开始时可以施展一次魔法，而每一分钟过后排在队伍最前面的猫咪就会离开队伍（这意味这啾啾会先交换位置然后队伍才开始移动）。
  >因为等会还得去买饺子所以啾啾会尽可能地与自身前方比它可爱且未出队的小猫交换位置（可以证明交换后必定更快买到酱油），现在啾啾想请你帮它计算出它需要多久才能买到酱油离开。

* ## <font size=4 face=粗体>思路</font>

  设x为啾啾的可爱值，从后往前将大于x的数压入栈，设置指针p指向0
  每次操作，先从栈中取出交换的值
    * 如果这个值比p大，说明可以交换，
    * 否则说明不能交换，那么加上p和目前啾啾的距离之差，即是答案
    * 若栈为空，同2

* ## <font size=4 face=粗体>代码</font>

  ```python
  '''
  Author: NEFU AB-IN
  Date: 2022-04-08 21:35:57
  FilePath: \ACM\ACnowcoder\2022.4.8\c.py
  LastEditTime: 2022-04-08 21:35:58
  '''
  n = int(input())

  a = list(map(int, input().split()))
  x = int(input())

  a = [0, *a]

  index = n + 1
  p = 0
  stk = []

  for i in range(1, n + 1):
      if a[i] > x:
          stk.append(i)
  ans = 0
  while True:
      if stk:
          tmp = stk[-1]
          if p < tmp:
              index = tmp
              stk.pop()
              ans += 1
          else:
              ans += max(0, index - p)
              print(ans)
              exit(0)
      else:
          ans += max(0, index - p)
          print(ans)
          exit(0)
      p += 1
  ```