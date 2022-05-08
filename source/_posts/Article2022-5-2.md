---
title: Windows C++ 对拍
tags:
  - 对拍
categories:
  - [C++]
  - [Project]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
photos:
  - https://oss.ab-in.cn/Pictures/duipai2.png
date: 2022-05-03 21:41:10
---

{% note info %}
**摘要**
Windows C++ 对拍
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

@[TOC](文章目录)

# <font color=#6495ED size=6 >Windows C++ 对拍</font>

* ## <font color=#FFA500 size=5>前言</font>

  在比赛时，对对拍的掌握还是比较必要的
  * **基本架构：**
    ```txt
    std.cpp   自己写的正解（可能不对）
    bl.cpp    暴力解法（保证正确）
    mkd.cpp   生成数据的程序
    dp.bat    对拍执行的脚本
    1.txt     生成的输入
    2.txt     std的输出
    3.txt     bl的输出
    ```
    ![duipai1](https://oss.ab-in.cn/Pictures/duipai1.png)
  * **基本思路：**
    先对这三个程序编译，利用mkd.cpp造的数据，分别输入进std.cpp和bl.cpp，输出的结果进行比对，如果不对就停下

* ## <font color=#FFA500 size=5>举例</font>
  
  以判断一个数是否为质数举例

  **std.cpp**

  ```cpp
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define SZ(X) ((int)(X).size())
  #define ALL(X) (X).begin(), (X).end()
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;

  const int INF = 0x3f3f3f3f;
  const int N = 1e6 + 10;
  int n;

  bool judge(int x)
  {
      if (x == 1)
          return false;
      for (int i = 2; i < n / i; ++i)
      {
          if (x % i == 0)
              return false;
      }
      return true;
  }

  signed main()
  {
      IOS;
      cin >> n;
      cout << judge(n);
      return 0;
  }
  ```

  ****

  **bl.cpp**

  ```cpp
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define SZ(X) ((int)(X).size())
  #define ALL(X) (X).begin(), (X).end()
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;

  const int INF = 0x3f3f3f3f;
  const int N = 1e6 + 10;
  int n;

  bool judge(int x)
  {
      if (x == 1)
          return false;
      for (int i = 2; i < n; ++i)
      {
          if (x % i == 0)
              return false;
      }
      return true;
  }

  signed main()
  {
      IOS;
      cin >> n;
      cout << judge(n);
      return 0;
  }
  ```
  ****

  **mkd.cpp**

  `srand(time(0));`           生成随机种子
  `rand() % 10000 + 1`        生成 1 到 10000的随机数
  `random_shuffle(a, a + n)`  对a数组随机排列
  ```cpp
  #include <bits/stdc++.h>
  using namespace std;
  #define int long long
  #define SZ(X) ((int)(X).size())
  #define ALL(X) (X).begin(), (X).end()
  #define IOS                                                                                                            \
      ios::sync_with_stdio(false);                                                                                       \
      cin.tie(0);                                                                                                        \
      cout.tie(0);
  #define DEBUG(X) cout << #X << ": " << X << endl;
  typedef pair<int, int> PII;

  const int INF = 0x3f3f3f3f;
  const int N = 1e6 + 10;
  int n;

  signed main()
  {
      IOS;
      srand(time(0));
      cout << rand() % 10000 + 1;
      return 0;
  }
  ```

  ****

  **dp.bat**
  前三行时编译，后三行是循环执行
  （背过即可）
  ```bat
  g++ -Wall -std=c++20 std.cpp -o std
  g++ -Wall -std=c++20 bl.cpp -o bl
  g++ -Wall -std=c++20 mkd.cpp -o mkd

  :loop
      mkd.exe > 1.txt
      std.exe < 1.txt > 2.txt
      bl.exe < 1.txt > 3.txt
      fc 2.txt 3.txt

  if not errorlevel 1 goto loop
  pause
  goto loop
  ```

  最后运行脚本即可，结果如下
  ![duipai2](https://oss.ab-in.cn/Pictures/duipai2.png)

  如果遇到错，结果如下
  ![duipai3](https://oss.ab-in.cn/Pictures/duipai3.png)
  此时先不要动，错误的数据就在1.txt中，可以去调试；调试完了，在退出重新运行脚本即可