---
title: 654. 最大二叉树
tags:
  - Leetcode
  - 每日一题
  - 笛卡尔树
  - 单调栈
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
date: 2022-08-29 16:54:28
---


{% note info %}
**摘要**
Title: 654. 最大二叉树
Tag: 笛卡尔树、单调栈
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/maximum-binary-tree/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>654. 最大二叉树</font>

* ## <font size=4 face=粗体>题意</font>

  >给定一个不重复的整数数组 nums 。 最大二叉树 可以用下面的算法从 nums 递归地构建:
  >创建一个根节点，其值为 nums 中的最大值。
  >递归地在最大值 左边 的 子数组前缀上 构建左子树。
  >递归地在最大值 右边 的 子数组后缀上 构建右子树。
  >返回 nums 构建的 最大二叉树 。

* ## <font size=4 face=粗体>思路</font>

  题意为，构建最大笛卡尔树，即**中序遍历为原数组，且满足最大堆的性质**
  * **普通做法** $O(n^2)$
    正常进行递归建树即可

  * **单调栈** $O(n)$

    **笛卡尔树最常见的优化方案**
    如果遍历到第$i$个数，必然这个数是在**建完之后的树的右链的最后面的点**（保证是中序遍历的最后一个点）
    * 情况1：$a[i] > max$ (max代表前面的最大值，也就是原根节点)
      那么把$a[i]$作为树的根节点就可以了，之前的树作为$a[i]$的左儿子
      ![1](https://oss.ab-in.cn/Pictures/654-1.jpg)
    * 情况2：$a[i] < max$
      在右链从下往上找（也就是从小到大），找到第一个比$a[i]$大的数
      * 用$a[i]$取代子树的位置
      * 把子树放到$a[i]$的左儿子上
      ![2](https://oss.ab-in.cn/Pictures/654-2.jpg)
      实现的话，可以将右链的数存到一个**单调递减栈**里面，如果栈顶比$a[i]$小，就需要弹出

* ## <font size=4 face=粗体>代码</font>

  **普通做法**
  ```cpp
  /**
  * Definition for a binary tree node.
  * struct TreeNode {
  *     int val;
  *     TreeNode *left;
  *     TreeNode *right;
  *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
  *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
  *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
  * };
  */
  // ---------------------
  #define N n + 100
  #define SZ(X) ((int)(X).size())
  #define DEBUG(X) cout << #X << ": " << X << '\n'
  typedef pair<int, int> PII;

  static int IOS = []() {
      ios::sync_with_stdio(false);
      cin.tie(nullptr);
      cout.tie(nullptr);
      return 0;
  }();

  class Solution
  {
    public:
      TreeNode *constructMaximumBinaryTree(vector<int> &nums)
      {
          auto findmax = [&](int l, int r) {
              int mx = nums[l], id = l;
              for (int i = l + 1; i <= r; ++i)
              {
                  if (nums[i] > mx)
                      mx = nums[i], id = i;
              }
              return id;
          };
          function<TreeNode *(int, int)> dfs = [&](int l, int r) {
              if (l > r)
                  return (TreeNode *)nullptr;
              int k = findmax(l, r);
              TreeNode *tree = new TreeNode(nums[k]);
              tree->left = dfs(l, k - 1);
              tree->right = dfs(k + 1, r);
              return tree;
          };

          return dfs(0, SZ(nums) - 1);
      }
  };

  // ---------------------
  ```

  ****

  **单调栈**

  ```cpp
      TreeNode *constructMaximumBinaryTree(vector<int> &nums)
      {
          stack<TreeNode *> stk;
          for (int x : nums)
          {
              auto node = new TreeNode(x);
              while (SZ(stk) && stk.top()->val < x)
              {
                  node->left = stk.top(); // 每次都指，while每次更新，最后的就是最优的
                  stk.pop();
              }
              if (SZ(stk))
                  stk.top()->right = node;
              stk.push(node);
          }

          while (SZ(stk) > 1)
              stk.pop();
          return stk.top(); // 此时栈顶就是根
      }
  ```
