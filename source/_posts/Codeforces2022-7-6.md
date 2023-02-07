---
title: Codeforces Round 799 (Div. 4)
tags:
  - Codeforces
  - 哈希表
  - 三数之和
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
date: 2022-07-06 11:37:57
---

{% note info %}
**摘要**
Title: Codeforces Round 799 (Div. 4)
Tag: 哈希表，三数之和
Problem: A, B, C, D, E, F, G, H
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>
  <font color=#FFA500 size=5 face=楷体>[B站直播录像！](https://www.bilibili.com/video/BV1Wj411M7GW/)</font>


<font color=#FFA500 size=5 face=楷体>[Link](https://codeforces.com/contest/1692)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6 >Codeforces Round 799 (Div. 4)</font>

* ## <font color=#FFA500 size=5>A. Marathon</font>

  * ### <font size=4 face=粗体>题意</font>

    >You are given four distinct integers $a$, $b$, $c$, $d$. Timur and three other people are running a marathon. The value $a$ is the distance that Timur has run and $b$, $c$, $d$ correspond to the distances the other three participants ran. Output the number of participants in front of Timur.


  * ### <font size=4 face=粗体>思路</font>

    比较大小即可

  * ### <font size=4 face=粗体>代码</font>
    ```cpp
    // Problem: A. Marathon
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-15 23:46:47
    // URL: https://codeforces.com/contest/1692/problem/A
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = 0x3f3f3f3f;
    const int N = 1e6 + 10;

    void solve()
    {
        int a, b, c, d;
        cin >> a >> b >> c >> d;
        cout << (b > a) + (c > a) + (d > a) << '\n';
    }

    signed main()
    {
        IOS;
        int t;
        cin >> t;
        while (t--)
        {
            solve();
        }
        return 0;
    }
    ```
  

* ## <font color=#FFA500 size=5>B. All Distinct</font>

  * ### <font size=4 face=粗体>题意</font>

    >Sho has an array $a$ consisting of $n$ integers. An operation consists of choosing two distinct indices $i$ and $j$ and removing $a_i$ and $a_j$ from the array.For example, for the array $[2, 3, 4, 2, 5]$, Sho can choose to remove indices $1$ and $3$. After this operation, the array becomes $[3, 2, 5]$. Note that after any operation, the length of the array is reduced by two.After he made some operations, Sho has an array that has only distinct elements. In addition, he made operations such that the resulting array is the longest possible. More formally, the array after Sho has made his operations respects these criteria:   No pairs such that ($i < j$) and $a_i = a_j$ exist.  The length of $a$ is maximized. Output the length of the final array.


  * ### <font size=4 face=粗体>思路</font>

    **每次去除两个数，求整个数列无不重复的元素的数列最长长度**

    求出元素种类$cnt$，看$n-cnt$是奇数还是偶数，是奇数的话就会多减去一个

  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: B. All Distinct
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-15 23:46:48
    // URL: https://codeforces.com/contest/1692/problem/B
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = 0x3f3f3f3f;
    const int N = 1e6 + 10;

    void solve()
    {
        int n;
        cin >> n;

        set<int> s;
        for (int i = 1; i <= n; ++i)
        {
            int x;
            cin >> x;
            s.insert(x);
        }

        int cnt = SZ(s);

        if ((n - cnt) & 1)
            cout << cnt - 1 << '\n';
        else
            cout << cnt << '\n';
        return;
    }

    signed main()
    {
        IOS;
        int t;
        cin >> t;
        while (t--)
        {
            solve();
        }
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>C. Where's the Bishop?</font>

  * ### <font size=4 face=粗体>题意</font>

    >Mihai has an $8 \times 8$ chessboard whose rows are numbered from $1$ to $8$ from top to bottom and whose columns are numbered from $1$ to $8$ from left to right.Mihai has placed exactly one bishop on the chessboard. The bishop is not placed on the edges of the board. (In other words, the row and column of the bishop are between $2$ and $7$, inclusive.)The bishop attacks in all directions diagonally, and there is no limit to the distance which the bishop can attack. Note that the cell on which the bishop is placed is also considered attacked.     
    >An example of a bishop on a chessboard. The squares it attacks are marked in red. Mihai has marked all squares the bishop attacks, but forgot where the bishop was! Help Mihai find the position of the bishop.

  * ### <font size=4 face=粗体>思路</font>


    找除了边缘的点，满足四个对角和自己都被占的点即可


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: C. Where's the Bishop?
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-15 23:46:49
    // URL: https://codeforces.com/contest/1692/problem/C
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = 0x3f3f3f3f;
    const int N = 10;

    char a[N][N];

    int dir[5][2] = {{0, 0}, {1, 1}, {1, -1}, {-1, -1}, {-1, 1}};

    void solve()
    {
        for (int i = 1; i <= 8; ++i)
        {
            for (int j = 1; j <= 8; ++j)
            {
                cin >> a[i][j];
            }
        }
        auto judge = [&](int x, int y) {
            for (int i = 0; i < 5; ++i)
            {
                int x1 = x + dir[i][0];
                int y1 = y + dir[i][1];
                if (a[x1][y1] == '#' && x1 >= 1 && x1 <= 8 && y1 >= 1 && y1 <= 8)
                {
                    continue;
                }
                else
                {
                    return 0;
                }
            }
            return 1;
        };

        for (int i = 2; i <= 7; ++i)
        {
            for (int j = 2; j <= 7; ++j)
            {
                if (judge(i, j))
                {
                    cout << i << " " << j << '\n';
                    return;
                }
            }
        }

        return;
    }

    signed main()
    {
        IOS;
        int t;
        cin >> t;
        while (t--)
        {
            solve();
        }
        return 0;
    }
    ```


* ## <font color=#FFA500 size=5>D. The Clock</font>

  * ### <font size=4 face=粗体>题意</font>

    >Victor has a 24-hour clock that shows the time in the format "HH:MM" (00 $\le$ HH $\le$ 23, 00 $\le$ MM $\le$ 59). He looks at the clock every $x$ minutes, and the clock is currently showing time $s$. How many different palindromes will Victor see in total after looking at the clock every $x$ minutes, the first time being at time $s$?For example, if the clock starts out as 03:12 and Victor looks at the clock every $360$ minutes (i.e. every $6$ hours), then he will see the times 03:12, 09:12, 15:12, 21:12, 03:12, and the times will continue to repeat. Here the time 21:12 is the only palindrome he will ever see, so the answer is $1$.A palindrome is a string that reads the same backward as forward. For example, the times 12:21, 05:50, 11:11 are palindromes but 13:13, 22:10, 02:22 are not.

  * ### <font size=4 face=粗体>思路</font>

    题意就是，从某一时刻开始，每次经过一定的间隔，问能经过多少个回文的时刻？

    思路就是，从某一时刻开始，将其放入set中，当出现set中能找到的时刻时，说明存在循环了，这个时候return即可


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: D. The Clock
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-15 23:46:50
    // URL: https://codeforces.com/contest/1692/problem/D
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = 0x3f3f3f3f;
    const int N = 1e6 + 10;

    void solve()
    {
        int h, m, d;
        scanf("%d:%d %d", &h, &m, &d);

        auto ff = [&](int ans) {
            int h = ans / 60;
            int m = ans % 60;
            string sh = to_string(h);

            if (h % 10 == m / 10 && h / 10 == m % 10)
                return 1;
            return 0;
        };

        set<int> s;
        int cnt = 0;
        int ans = h * 60 + m;
        while (s.find(ans) == s.end())
        {
            s.insert(ans);
            if (ff(ans))
                cnt += 1;

            ans += d;
            ans %= 1440;
        }
        cout << cnt << '\n';
        return;
    }

    signed main()
    {
        int t;
        cin >> t;
        while (t--)
        {
            solve();
        }
        return 0;
    }
    ```


* ## <font color=#FFA500 size=5>E. Binary Deque</font>

  * ### <font size=4 face=粗体>题意</font>

    >Slavic has an array of length $n$ consisting only of zeroes and ones. In one operation, he removes either the first or the last element of the array. What is the minimum number of operations Slavic has to perform such that the total sum of the array is equal to $s$ after performing all the operations? In case the sum $s$ can't be obtained after any amount of operations, you should output -1.

  * ### <font size=4 face=粗体>思路</font>

    给一个数组，有一种操作，只能去除第一个或最后一个元素，问多少次操作后，数组的和等于题目给的值

    思路就是**双指针**，只能去除两边的元素，也就是让我们找一个最长的连续的空间，使它的和等于要求的值即可


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: E. Binary Deque
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-29 22:47:31
    // URL: https://codeforces.com/contest/1692/problem/E
    // Memory Limit: 256 MB
    // Time Limit: 2000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = INT_MAX;
    const int N = 1e6 + 10;

    void solve()
    {
        int n, s;
        cin >> n >> s;
        vector<int> a(n);
        for (int i = 0; i < n; ++i)
        {
            cin >> a[i];
        }
        int sum = accumulate(a.begin(), a.end(), 0);
        if (sum < s)
        {
            cout << "-1\n";
            return;
        }
        int cnt = 0, mx = 0;
        for (int i = 0, j = 0; i < n; ++i)
        {
            cnt += (a[i] == 1);
            while (j < i && cnt > s)
            {
                cnt -= (a[j++] == 1);
                if (cnt == s)
                    mx = max(mx, i - j + 1);
            }
            if (cnt == s)
                mx = max(mx, i - j + 1);
        }
        cout << n - mx << '\n';
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
        {
            solve();
        }
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>F. 3SUM</font>

  * ### <font size=4 face=粗体>题意</font>

    >Given an array $a$ of positive integers with length $n$, determine if there exist three distinct indices $i$, $j$, $k$ such that $a_i + a_j + a_k$ ends in the digit $3$.

  * ### <font size=4 face=粗体>思路</font>

    题意就是，给定长度为n的数组a，问是否存在三个数的加和，它的末位为3

    乍一看类似于**N数之和**，即**N SUM**的题，其实不然，因为他并**不是要求最后的和为多少，而是要求最后一位是多少**，所以不能采取相同的思路

    我们注意到
      * 只考虑**个位**，那么我们只留每个数的个位即可
      * 只考虑三个数的加和，那么0~9的个位数，每个数只保留最多三个即可
      * 再遍历这$n$ 最多等于 $30$, $O(n^3)$复杂度，即可

  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: F. 3SUM
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-29 22:47:32
    // URL: https://codeforces.com/contest/1692/problem/F
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = INT_MAX;
    const int N = 1e6 + 10;

    void solve()
    {
        int n, x;
        cin >> n;
        unordered_map<int, int> d;
        vector<int> a;
        for (int i = 0; i < n; ++i)
        {
            cin >> x;
            x %= 10;
            if (++d[x] > 3)
                d[x] = 3;
            else
                a.push_back(x);
        }
        for (int i = 0; i < SZ(a); ++i)
        {
            for (int j = i + 1; j < SZ(a); ++j)
            {
                for (int k = j + 1; k < SZ(a); ++k)
                {
                    if ((a[i] + a[j] + a[k]) % 10 == 3)
                    {
                        puts("YES");
                        return;
                    }
                }
            }
        }
        puts("NO");
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
        {
            solve();
        }
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>G. 2^Sort</font>

  * ### <font size=4 face=粗体>题意</font>

    >Given an array $a$ of length $n$ and an integer $k$, find the number of indices $1 \leq i \leq n - k$ such that the subarray $[a_i, \dots, a_{i+k}]$ with length $k+1$ (not with length $k$) has the following property:   If you multiply the first element by $2^0$, the second element by $2^1$, ..., and the ($k+1$)-st element by $2^k$, then this subarray is sorted in strictly increasing order.  More formally, count the number of indices $1 \leq i \leq n - k$ such that 
    >$$2^0 \cdot a_i < 2^1 \cdot a_{i+1} < 2^2 \cdot a_{i+2} < \dots < 2^k \cdot a_{i+k}.$$ 


  * ### <font size=4 face=粗体>思路</font>

    题意为，在数组a中，存在多少个以i为下标的，长度为k+1的满足条件的数列。满足的条件是**前一个数需要小于后一个数的二倍**

    一道**思维差分**题
      * 首先可以知道，如果存在**前一个数需要大于等于后一个数的二倍**的组合，那么一定不会有数列包含它们
      * 那么我们只需要把以i为下标，k+1长度的，包含这种组合的序列，进行标记即可，找寻规律用**差分**进行标记
      * 最后找寻没被标记的且满足条件的下标i即可



  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: G. 2^Sort
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-29 22:47:33
    // URL: https://codeforces.com/contest/1692/problem/G
    // Memory Limit: 256 MB
    // Time Limit: 1000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = INT_MAX;
    const int N = 1e6 + 10;

    void solve()
    {
        int n, k;
        cin >> n >> k;
        vector<int> a(n + 1), b(n + 1);
        for (int i = 1; i <= n; ++i)
        {
            cin >> a[i];
            if (i > 1 && a[i - 1] >= 2 * a[i])
            {
                // DEBUG(i - k + 1)
                // DEBUG(b[i - k + 1])
                b[max(1LL, i - k)]++;
                b[i]--;
            }
        }
        for (int i = 1; i <= n; ++i)
        {
            b[i] += b[i - 1];
        }
        int ans = 0;
        for (int i = 1; i <= n; ++i)
        {
            if (!b[i] && i + k <= n)
            {
                ans++;
            }
        }
        cout << ans << '\n';
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
        {
            solve();
        }
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>H. Gambling</font>

  * ### <font size=4 face=粗体>题意</font>

    >Marian is at a casino. The game at the casino works like this.Before each round, the player selects a number between $1$ and $10^9$. After that, a dice with $10^9$ faces is rolled so that a random number between $1$ and $10^9$ appears. If the player guesses the number correctly their total money is doubled, else their total money is halved. Marian predicted the future and knows all the numbers $x_1, x_2, \dots, x_n$ that the dice will show in the next $n$ rounds. He will pick three integers $a$, $l$ and $r$ ($l \leq r$). He will play $r-l+1$ rounds (rounds between $l$ and $r$ inclusive). In each of these rounds, he will guess the same number $a$. At the start (before the round $l$) he has $1$ dollar.Marian asks you to determine the integers $a$, $l$ and $r$ ($1 \leq a \leq 10^9$, $1 \leq l \leq r \leq n$) such that he makes the most money at the end.Note that during halving and multiplying there is no rounding and there are no precision errors. So, for example during a game, Marian could have money equal to $\dfrac{1}{1024}$, $\dfrac{1}{128}$, $\dfrac{1}{2}$, $1$, $2$, $4$, etc. (any value of $2^t$, where $t$ is an integer of any sign).

  * ### <font size=4 face=粗体>思路</font>

    题意就是，找到包含**价值最高，且最短**的区间
    所谓价值最高是指此区间越多包含x，价值越高，x为任意值

    思路就是哈希表
      * 把每个数的下标都存起来，可以开一个 <int, vector<int> >的哈希表
      * 再对每种x的下标进行遍历，每次减掉两下标之间的差（即不是x的），再加上1（因为遍历到了一个x）
        * 如果完成上面操作，价值小于1了，说明连初始值都不如，那么就需要将价值置1，并选定其为新的起点
      * 每次进行更新最大价值，并相继更新区间的左右边界

    **注意，此题数据会卡$unorderd\_map$，所以建议用map，或者自己写的哈希函数**


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    // Problem: H. Gambling
    // Contest: Codeforces Round #799 (Div. 4)
    // Author: NEFU AB-IN
    // Edit Time:2022-06-29 22:47:34
    // URL: https://codeforces.com/contest/1692/problem/H
    // Memory Limit: 256 MB
    // Time Limit: 2000 ms

    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #define SZ(X) ((int)(X).size())
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(0);                                                                                                        \
        cout.tie(0);
    #define DEBUG(X) cout << #X << ": " << X << endl;
    typedef pair<int, int> PII;

    const int INF = INT_MAX;
    const int N = 1e6 + 10;

    struct custom_hash
    {
        static uint64_t splitmix64(uint64_t x)
        {
            x += 0x9e3779b97f4a7c15;
            x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9;
            x = (x ^ (x >> 27)) * 0x94d049bb133111eb;
            return x ^ (x >> 31);
        }

        size_t operator()(uint64_t x) const
        {
            static const uint64_t FIXED_RANDOM = chrono::steady_clock::now().time_since_epoch().count();
            return splitmix64(x + FIXED_RANDOM);
        }
    };

    void solve()
    {
        int n;
        cin >> n;
        vector<int> a(n);

        // map<int, vector<int>> b; // 会被卡unordered_map

        unordered_map<int, vector<int>, custom_hash> b; // 手写hash也可以

        for (int i = 0; i < n; ++i)
        {
            cin >> a[i];
            b[a[i]].emplace_back(i);
        }
        int mx = 0, l = 0, r = 0, res = a[0];
        for (auto [x, v] : b)
        {
            int s = v[0], last = v[0], ans = 1;
            for (int i = 1; i < SZ(v); ++i)
            {

                int num = v[i] - last - 1;
                last = v[i];

                ans -= num; // 减去中间值
                ans++;      // 加上下一值
                if (ans < 1)
                { // 如果ans < 1，那么就要有新的开始
                    s = v[i];
                    ans = 1;
                }

                if (mx < ans)
                {
                    mx = ans;
                    l = s;
                    r = last;
                    res = x;
                }
            }
        }
        cout << res << " " << l + 1 << " " << r + 1 << "\n";

        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
        {
            solve();
        }
        return 0;
    }
    ```
