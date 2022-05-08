---
title: Conda 如何退出base环境
tags:
  - Conda
  - Python3
categories:
  - [Project]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2022-05-03 21:19:50
---

{% note info %}
**摘要**
Conda 如何退出base环境
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>


@[TOC](文章目录)

# <font color=#6495ED size=6 >Conda 如何退出base环境</font>

* ## <font color=#FFA500 size=5>前言</font>

  当初始化conda环境时，比如我是用的powershell，在执行
  ```powershell
  conda init
  ```
  之后，重启powershell，会发现此处出现一个脚本
  ![conda1](https://oss.ab-in.cn/Pictures/conda1.png)
  它是在打开powershell的同时执行的脚本，用来默认启动base环境

  但是，如果一启动就在base环境，会影响exe文件的执行，比如
  ![conda2](https://oss.ab-in.cn/Pictures/conda2.png)
  所以必须退出base环境，会很麻烦；但是删除脚本，每次还需要init，并且重启shell

* ## <font color=#FFA500 size=5>方案</font>

  这时只需要配置一下即可，让它一开始不启动base即可
  ```powershell
  conda config --set auto_activate_base false
  ```
  这样如果想用conda，直接手动激活base或者其他环境即可