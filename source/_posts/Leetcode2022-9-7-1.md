---
title: 1379. 找出克隆二叉树中的相同节点
tags:
  - Leetcode
  - 每日一题
  - DFS
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
date: 2022-09-07 16:21:45
---


{% note info %}
**摘要**
Title: 1379. 找出克隆二叉树中的相同节点
Tag: DFS
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://leetcode.cn/problems/find-a-corresponding-node-of-a-binary-tree-in-a-clone-of-that-tree/)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>1379. 找出克隆二叉树中的相同节点</font>

* ## <font size=4 face=粗体>题意</font>

  >给你两棵二叉树，原始树 original 和克隆树 cloned，以及一个位于原始树 original 中的目标节点 target。
  >其中，克隆树 cloned 是原始树 original 的一个 副本 。
  >请找出在树 cloned 中，与 target 相同 的节点，并返回对该节点的引用（在 C/C++ 等有指针的语言中返回 节点指针，其他语言返回节点本身）。


* ## <font size=4 face=粗体>思路</font>

  DFS找值即可，这里提供两个DFS版本
  * 第一版是返回void的DFS
  * 第二版是直接返回结果的

* ## <font size=4 face=粗体>代码</font>

  版本1
  ```cpp
  /**
  * Definition for a binary tree node.
  * struct TreeNode {
  *     int val;
  *     TreeNode *left;
  *     TreeNode *right;
  *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
  * };
  */

  class Solution {
  public:
      TreeNode* ans = new TreeNode();
      void dfs(TreeNode* root, int val){
          if(!root) return;
          
          if(root->val == val){
              ans = root;
              return;
          }    
          dfs(root->left, val);
          dfs(root->right, val);
      }
      TreeNode* getTargetCopy(TreeNode* original, TreeNode* cloned, TreeNode* target) {
          
          dfs(cloned, target->val);
          return ans;
      }
  };
  ```

  ****

  版本2

  ```cpp
  /**
  * Definition for a binary tree node.
  * struct TreeNode {
  *     int val;
  *     TreeNode *left;
  *     TreeNode *right;
  *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
  * };
  */

  class Solution {
  public:
      
      TreeNode* dfs(TreeNode* root, int val){
          if(!root) return nullptr;
          if(root->val == val){
              return root;
          }    
          auto left = dfs(root->left, val);
          if(left) return left;
          auto right = dfs(root->right, val);
          if(right) return right;
          
          return nullptr;
      }
      TreeNode* getTargetCopy(TreeNode* original, TreeNode* cloned, TreeNode* target) {
          return dfs(cloned, target->val);
      }
  };
  ```