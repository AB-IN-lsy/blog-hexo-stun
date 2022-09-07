---
title: 1373. 二叉搜索子树的最大键值和
tags:
  - Leetcode
  - 每日一题
  - DFS
  - BST
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
date: 2022-09-07 15:57:57
---


{% note info %}
**摘要**
Title: 1373. 二叉搜索子树的最大键值和
Tag: DFS、BST
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/maximum-sum-bst-in-binary-tree/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1373. 二叉搜索子树的最大键值和</font>

* ## <font size=4 face=粗体>题意</font>

  >给你一棵以 root 为根的 二叉树 ，请你返回 任意 二叉搜索子树的最大键值和。

* ## <font size=4 face=粗体>思路</font>

  判断一颗树是否是二叉搜索树的充分条件:

  * 根节点值大于左子树最大值，说明比左子树所有元素都大
  * 根节点值小于右子树最小值，说明比右子树所有元素都小
  * 左子树是二叉搜索树
  * 右子树是二叉搜索树
  
  满足上面四个条件，我们就推断出当前树是一颗二叉搜索树。
  所以我们可以在每层递归里记录四个值:

  * **当前树的最小值**
  * **当前树的最大值**
  * **当前树的和**
  * **当前树是否是二叉搜索树**
  
  当前调用层的每个值都可以根据它的左子树和右子树返回的数组，以及它本身的值来更新。


* ## <font size=4 face=粗体>代码</font>

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
  class Solution {
  public:
      int ans = 0;
      
      
      // 返回值:            {min, max, sum, isBiSearchTree}
      vector<int> dfs(TreeNode* root){
          if(!root) return {INT_MAX, INT_MIN, 0, true}; // 初始化
          // 比如最小值初始化为最大值，这样可以一直满足 val < right[0]这个不等式
          // 将isB也初始化为true，方便判断叶节点的情况
          auto left = dfs(root->left);
          auto right = dfs(root->right);
          
          int val = root->val;
          int sum = left[2] + right[2] + val;
          bool isB = false;
          
          // 判断是否为二叉搜索树，四个条件
          if(val > left[1] && val < right[0]){
              if(left[3] && right[3]) isB = true;
          }
          
          // 更新值
          if(isB) ans = max(ans, sum);
          int mx = max({left[1], right[1], val});
          int mn = min({left[0], right[0], val});
          
          return {mn, mx, sum, isB};
      }
      
      
      
      int maxSumBST(TreeNode* root) {
          dfs(root);
          return ans;
      }
  };
  ```