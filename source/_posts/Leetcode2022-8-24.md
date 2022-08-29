---
title: 641. 设计循环双端队列
tags:
  - Leetcode
  - 每日一题
  - 双端队列
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
date: 2022-08-24 14:16:43
---


{% note info %}
**摘要**
Title: 641. 设计循环双端队列
Tag: 双端队列
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/design-circular-deque/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>641. 设计循环双端队列</font>

* ## <font size=4 face=粗体>题意</font>

  >设计实现双端队列。
  >实现 MyCircularDeque 类:

* ## <font size=4 face=粗体>思路</font>

  数组模拟队列
  根据循环队列的定义，队列判空的条件是 $\textit{front}=\textit{rear}front=rear$，而队列判满的条件是 $\textit{front} = (\textit{rear} + 1) \bmod \textit{capacity}front=(rear+1)modcapacity$


* ## <font size=4 face=粗体>代码</font>

  ```cpp
  class MyCircularDeque
  {
    public:
  #define SZ(X) ((int)(X).size())
      vector<int> q;
      int hh = 0, tt = 0;
      // 左闭右开，也就是tt表示队列最后一个元素的下一个

      int get(int x)
      {
          return (x + SZ(q)) % SZ(q);
      }

      MyCircularDeque(int k)
      {
          q.resize(k + 1);
          // 用tt和hh的差值表示状态，从0到k需要表示k+1种状态，所以需要开k+1大小的数组
      }

      bool insertFront(int value)
      {
          if (isFull())
              return false;
          hh = get(hh - 1);
          q[hh] = value;
          return true;
      }

      bool insertLast(int value)
      {
          if (isFull())
              return false;
          q[tt] = value;
          tt = get(tt + 1);
          // 先加元素，因为tt是最后一个元素的下一个
          return true;
      }

      bool deleteFront()
      {
          if (isEmpty())
              return false;
          hh = get(hh + 1);
          return true;
      }

      bool deleteLast()
      {
          if (isEmpty())
              return false;
          tt = get(tt - 1);
          return true;
      }

      int getFront()
      {
          if (isEmpty())
              return -1;
          return q[hh];
      }

      int getRear()
      {
          if (isEmpty())
              return -1;
          return q[get(tt - 1)];
      }

      bool isEmpty()
      {
          return hh == tt;
      }

      bool isFull()
      {
          return hh == get(tt + 1);
      }
  };

  /**
  * Your MyCircularDeque object will be instantiated and called as such:
  * MyCircularDeque* obj = new MyCircularDeque(k);
  * bool param_1 = obj->insertFront(value);
  * bool param_2 = obj->insertLast(value);
  * bool param_3 = obj->deleteFront();
  * bool param_4 = obj->deleteLast();
  * int param_5 = obj->getFront();
  * int param_6 = obj->getRear();
  * bool param_7 = obj->isEmpty();
  * bool param_8 = obj->isFull();
  */
  ```