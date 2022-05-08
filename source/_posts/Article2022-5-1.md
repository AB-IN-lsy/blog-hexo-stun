---
title: Vscode 创建task并绑定快捷键教程
tags:
  - Vscode
  - task
categories:
  - [2022大三下学期]
  - [Project]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
photos: 
  - https://oss.ab-in.cn/Pictures/task1.png
reward: true
date: 2022-05-01 10:45:01
---

{% note info %}
**摘要**
Vscode 创建task并绑定快捷键教程
例子为创建新的文件
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

@[TOC](文章目录)

# <font color=#6495ED size=6 >Vscode 创建task并绑定快捷键教程</font>

  [有关的VSC变量引用](https://blog.csdn.net/hn_tzy/article/details/104652114)
  [Task部分json变量含义](https://blog.csdn.net/qq_53653262/article/details/120859147?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522165104850216781435435304%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=165104850216781435435304&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-5-120859147.142^v9^pc_search_result_cache,157^v4^control&utm_term=vscode+task&spm=1018.2226.3001.4187)
* ## <font color=#FFA500 size=5>Task</font>

  参考上面两个博客，应该是能创建出基本的Task了，建议在本目录下的`.vscode`中创建`task.json`
  我这里给出一个Task例子——**在当前目录下创建自定义文件**


  **确定目录**
  ```json
  "options": {
      "cwd": "${workspaceRoot}" //为了确定当前目录，其实默认就是当前根目录
  }
  ```
  ****
  **Task源码**
  ```json
  "tasks": [{
      "type": "shell", // 这里是设定task的类型，是你要执行shel命令，还是运行文件
      "label": "CreateNewFile", // 此task的名字
      "command": "cd.", // 此task的核心命令
      "windows": {
          "options": {
              "shell": { // 由于我的默认shell是pwsh,
              // 所以我这里可以采用更改成shell为cmd的方式，来执行接下来的命令
                  "executable": "cmd.exe",
                  "args": [
                      "/d", "/c"
                  ]
              }

          }
      },
      "args": [ // 代表后面需要传的参数，
      // 由于我们是要创建一个可选的文件，那么就需要输入你想创建的文件名字，这个variableID代表变量名
          ">${input:variableID}",
      ], 
      "options": { // 代表我们当前运行的命令，在我们目前打开的文件的文件夹中
          "cwd": "${fileDirname}",
      },
      // 下面这两个自动加上的
      "problemMatcher": [],
      "group": {
          "kind": "build",
          "isDefault": true
      }
  }],
  ```
  ****
  **处理variableID变量**

  ```json
  "inputs": [{
      "id": "variableID", // 代表我们要设定的变量名
      "type": "promptString", // 代表怎么输入，这里采用弹出来一个框
      "description": "Please input the file name: ", 
      "default": "main.cpp"// 如果直径按回车，默认main.cpp
  }],
  ```
  ****
  **整个Task.json不带注释**

  ```json
  {
      "options": {
          "cwd": "${workspaceRoot}"
      },
      "tasks": [{
          "type": "shell",
          "label": "CreateNewFile",
          "command": "cd.",
          "windows": {
              "options": {
                  "shell": {
                      "executable": "cmd.exe",
                      "args": [
                          "/d", "/c"
                      ]
                  }

              }
          },
          "args": [
              ">${input:variableID}",
          ],
          "options": {
              "cwd": "${fileDirname}",
          },
          "problemMatcher": [],
          "group": {
              "kind": "build",
              "isDefault": true
          }
      }],
      "inputs": [{
          "id": "variableID",
          "type": "promptString",
          "description": "Please input the file name: ",
          "default": "main.cpp"
      }],
      "version": "2.0.0"
  }
  ```

* ## <font color=#FFA500 size=5>绑定快捷键</font>

  * 打开`keybindings.json` 不出意外应该在 `C:\Users\你自己的用户名\AppData\Roaming\Code\User`下
  * 点右下角的**定义键绑定**
  * 代码
    ```json
    {
        "key": "ctrl+alt+z", // 你自定义的快捷键
        "command": "workbench.action.tasks.runTask", // 固定的！不用动！就是在你目录下runtask的意思
        "args": "CreateNewFile", // 你任务的名字
        "when": "editorTextFocus" // 当你按快捷键的时候
    },
    ```
  
  自此配置完成

  效果图
  ![task1](https://oss.ab-in.cn/Pictures/task1.png)
  ![task2](https://oss.ab-in.cn/Pictures/task2.png)

* ## <font color=#FFA500 size=5>杂话</font>

    其实初衷是看了某OI佬的CF实况，感觉这种用Task快捷键的方式很方便，就想尝试搞一下
    但没注意他用的是macOS，好像有可以用vscode打开文件的命令，而win是没有的
    也就是现在我们创建完文件，还是需要自己找到并点进去，而mac的命令可以做到直接打开
    这也算小小的遗憾吧~
