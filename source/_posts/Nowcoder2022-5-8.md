---
title: Nowcoder C. 涂墙
tags:
  - Nowcoder
  - bitset
  - 规律题
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
date: 2022-05-09 14:38:52
---


{% note info %}
**摘要**
Title: Nowcoder C. 涂墙
Tag: bitset、规律题
Memory Limit: 64 MB
Time Limit: 1000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/C)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder C. 涂墙</font>

* ## <font size=4 face=粗体>题意</font>

  >母牛哥有一桶油漆,把它用完可以给n平方米的墙涂上颜色.
  >母牛哥想要在墙上涂5个正方形(这些正方形的边长都是整数,单位是米),并且刚好把油漆用完.
  >母牛哥能做到吗?

* ## <font size=4 face=粗体>思路</font>

  * **思路1 找规律**
    可以先对结果进行初步打表，打出不能的数，打表代码
    ```python
    a = []
    for i in range(1, 200):
        a.append(i * i)

    vis = [0] * 200
    for i in range(1, 200):
        flag = 0
        for i1 in a:
            if i1 > i or flag: break
            for i2 in a:
                if i2 > i or flag: break
                for i3 in a:
                    if i3 > i or flag: break
                    for i4 in a:
                        if i4 > i or flag: break
                        for i5 in a:
                            if i5 > i: break
                            if i == i1 + i2 + i3 + i4 + i5:
                                vis[i] = 1
                                flag = 1
                                break
    for i in range(200):
        if vis[i] == 0:
            print(i, end=",")
    ```
    ```txt
    结果：0,1,2,3,4,6,7,9,10,12,15,18,33
    ```
    可以发现，前两百只有这几个数不能，可以推断后面的数都是yes

  * **思路2 bitset**
    采用bitset压位来做
    再来更新一下bitset的知识：
    * 采用bitset可以省8倍空间
    * 每个操作都是$O(log(N))$级别的
    ****
    **基本操作**
    ```cpp
    1.定义：
    bitset <N> s;
    表示一个N位的二进制数，<>中填写位数；

    2.位运算操作符：
    ~s: 返回对s每一位取反后的结果；
    &，|，^：返回对两个位数相同的bitset执行按位与、或、异或运算的结果；
    <<, >>:返回把一个bitset左移，右移若干位的结果.（补零）；

    ==，！=：比较两个位数相同的bitset代表的二进制数是否相等；

    3.[ ]操作符：
    s[k] :表示s的第k位，即可取值也可赋值，编号从0开始；

    4.count:
    s.count() 返回二进制串中有多少个1；

    5.any/none
    若s所有位都为0，则s.any()返回false，s.none()返回true；
    若s至少有一位为1，则s.any()返回true，s.none()返回false；

    6.set/rest/flip
    s.set()把s所有位变为1；
    s.set(k,v)把s的第k位改为v,即s[k]=v；
    s.reset()把s的所有位变为0.
    s.reset(k)把s的第k位改为0,即s[k]=0；
    s.flip()把s所有位取反.即s=~s；
    s.flip(k)把s的第k位取反，即s[k]^=1；

    7.test
    s.test(a) 等价于 s[a], 用来检测该bitset是否包含a这个数
    ```

    **思路为**：由于数据最大到1e6，那么平方数的底数最大1e3，所以我们开**两个**1e6的bitset——b1和b2，枚举1e3的平方数的底数，进行这个操作 `b1 |= b2 << (i * i)`，执行5次，每次log(N)查询结果即可
      * `b2 << (i * i)` 就是**让b2中所有值为1的数都加上 i*i**
        比如 b2中 `b2[1] = 1, b2[4] = 1`, 那么右移2位后，`b2[3] = 1, b2[7] = 1`
      * `b1 |= b2` 就是让b2中值为1的数，在b1中也为1


* ## <font size=4 face=粗体>代码</font>

  * **思路1  找规律**
    ```cpp
    #include <bits/stdc++.h>
    #define int long long
    using namespace std;

    signed main(){
        
        vector <int> v = {0,1,2,3,4,6,7,9,10,12,15,18,33};
        unordered_set<int> mp;
        for(auto i : v) mp.insert(i);
        
        int t;
        cin >> t;
        while(t --){
            int n;
            cin >> n;
            if(mp.count(n)) cout << "NO\n";
            else cout << "YES\n";
        }
        return 0;
    }
    ```

  ****
  * **思路2 bitset**

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

    const int N = 1e6 + 10, M = 1e3 + 10;

    signed main()
    {
        IOS;
        bitset<N> dp;
        dp.set(0); // 一开始将0处设为1

        for (int i = 1; i <= 5; ++i)
        {
            bitset<N> tmp;
            for (int j = 1; j < M; ++j)
            {
                tmp |= dp << (j * j);
            }
            dp = tmp; // 每次继承这一次的结果
        }

        int t;
        cin >> t;
        while (t--)
        {
            int n;
            cin >> n;
            cout << (dp.test(n) ? "YES" : "NO") << '\n';
        }
        return 0;
    }
    ```
