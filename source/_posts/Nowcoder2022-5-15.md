---
title: Nowcoder 牛牛的数列
tags:
  - Nowcoder
  - dp
  - 前缀
  - 后缀
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
date: 2022-05-15 20:20:16
---


{% note info %}
**摘要**
Title: Nowcoder 牛牛的数列
Tag: dp、前缀、后缀
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/problem/13134)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder 牛牛的数列</font>

* ## <font size=4 face=粗体>题意</font>

  >牛牛现在有一个n个数组成的数列,牛牛现在想取一个连续的子序列,并且这个子序列还必须得满足:最多只改变一个数,就可以使得这个连续的子序列是一个严格上升的子序列,牛牛想知道这个连续子序列最长的长度是多少。

* ## <font size=4 face=粗体>思路</font>

  需要预处理出来两个数组
  * `pre[i]` 表示 **以i为结束最长的上升子序列的长度**
  * `post[i]`表示 **以i为开始最长的上升子序列的长度**

  这样最大值的选取就显而易见了
  * **不改**`a[i]`， 那么就两个数值取最大值 `max(pre[i], post[i])`
  * **改** `a[i]`
    * **单方面** `max(pre[i - 1] + 1, post[i + 1] + 1)` 就是说取一个的，然后把`a[i]`这个数变成满足前一个的
    * **双方面** 如果 `a[i + 1] - a[i - 1] >= 2` 说明两个数之间能放一个数，那么就是 `pre[i - 1] + post[i + 1] + 1`
  
  这些数求个最大值即可
* ## <font size=4 face=粗体>代码</font>

  ```cpp
  #include <bits/stdc++.h>
  #define int long long
  #define SZ(X) ((int) X.size())
  using namespace std;

  signed main(){
      int n;
      cin >> n;
      vector<int> a(n);
      for(int i = 0; i < n; ++ i) cin >> a[i];
      
      vector<int> pre(n), post(n);
      int last = 0;
      // 以i为结束最长的上升子序列的长度
      for(int i = 0; i < n; ++ i){
          if(!i || a[i] > a[i - 1]){
              pre[i] = ++ last;
          }
          else{
              pre[i] = 1;
              last = 1;
          }
      }
      last = 0;
      // 以i为开始最长的上升子序列的长度
      for(int i = n - 1; i >= 0; -- i){
          if(i == n - 1 || a[i + 1] > a[i]){
              post[i] = ++ last;
          }
          else{
              post[i] = 1;
              last = 1;
          }
      }
      int ans = 1;
      for(int i = 0; i < n; ++ i){
          ans = max({ans, pre[i], post[i]});
          if(i) ans = max(ans, pre[i - 1] + 1);
          if(i != n - 1) ans = max(ans, post[i + 1] + 1);
          if(i && i != n - 1 && a[i + 1] - a[i - 1] >= 2) {
              ans = max(ans, pre[i - 1] + post[i + 1] + 1);
          }
      }
      cout << ans;
      return 0;
  }

  ```