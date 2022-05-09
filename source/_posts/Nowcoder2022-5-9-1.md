---
title: Nowcoder A. M形字符串
tags:
  - Nowcoder
  - 回文串
  - 字符串哈希
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
date: 2022-05-09 17:28:19
---


{% note info %}
**摘要**
Title: Nowcoder A. M形字符串
Tag: 回文串、字符串哈希
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/A)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder A. M形字符串</font>

* ## <font size=4 face=粗体>题意</font>

  >给一个长度为n的字符串(1<=n<=200000),他只包含小写字母
  >找到这个字符串多少个前缀是M形字符串.
  >M形字符串定义如下:
  >他由两个相同的回文串拼接而来,第一个回文串的结尾字符和第二个字符串的开始字符可以重叠,也就是以下都是M形字符串.
  >abccbaabccba(由abccba+abccba组成)
  >abcbaabcba(有abcba+abcba组成)
  >abccbabccba(由abccba+abccba组成组成,但是中间的1是共用的)
  >a(一个单独字符也算)

* ## <font size=4 face=粗体>思路</font>

  **判断回文串——字符串正向+反向哈希**

  判断这个字符串是不是两个回文串拼接成的，只需要判断
    * 这个字符串是不是回文
    * 这个拼接的是不是回文
  
  即可

* ## <font size=4 face=粗体>代码</font>

  ```cpp
  #include <bits/stdc++.h>

  using namespace std;
  #define ULL unsigned long long 
  #define SZ(X) ((int) X.size())
  const int P = 131;
  const int N = 2e5 + 10;

  ULL h[N], p[N], hr[N];


  int main(){
      p[0] = 1;
      string s;
      cin >> s;
      int n = SZ(s);
      s = " " + s;

      for(int i = 1; i <= n; ++ i){
          hr[i] = hr[i - 1] * P + s[n - i + 1] - '0';
          h[i] = h[i - 1] * P + s[i] - '0';
          p[i] = p[i - 1] * P;
      }
      
      auto get = [&] (ULL *h, int l, int r){
          return h[r] - h[l - 1] * p[r - l + 1];
      }; // 公用一个get函数

      
      auto check = [&] (int l, int r){
          return get(h, l, r) == get(hr, n - r + 1, n - l + 1);
      }; // 判断是否回文
      
      int ans = 0;
      for(int i = 1; i <= n; ++ i){
          if(check(1, i) && check(1, (i + 1) / 2)) ans ++;
      }
      cout << ans;
      
      return 0;
  }
  ```