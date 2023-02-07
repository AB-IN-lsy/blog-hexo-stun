---
title: Codeforces Round 849 (Div. 4) 
tags:
  - Codeforces
  - set
  - dp
categories:
  - [ACM]
  - [2023大四下学期]
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2023-02-04 13:58:37
---

{% note info %}
**摘要**
Title: Codeforces Round 799 (Div. 4)
Tag: set，dp
Problem: A, B, C, D, E, F, G1
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://codeforces.com/contest/1791)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6 >Codeforces Round 849 (Div. 4) </font>

* ## <font color=#FFA500 size=5>A	Codeforces Checking</font>

  * ### <font size=4 face=粗体>题意</font>

    >Given a lowercase Latin character (letter), check if it appears in the string codeforces codeforces .

  * ### <font size=4 face=粗体>思路</font>

    模拟


  * ### <font size=4 face=粗体>代码</font>
  
    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #undef int

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 1e5 + 10, INF = 0x3f3f3f3f;

    void solve()
    {
        char a;
        cin >> a;
        string s = "codeforces";
        for (auto x : s)
        {
            if (x == a)
            {
                cout << "YES\n";
                return;
            }
        }
        cout << "NO\n";
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>B. Following Directions</font>

  * ### <font size=4 face=粗体>题意</font>

    >略

  * ### <font size=4 face=粗体>思路</font>

    模拟

  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    /*
    * @Author: NEFU AB-IN
    * @Date: 2023-02-03 22:35:26
    * @FilePath: \CF\1791\b\b.cpp
    * @LastEditTime: 2023-02-03 22:40:58
    */
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #undef int

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 1e5 + 10, INF = 0x3f3f3f3f;

    void solve()
    {
        int n;
        cin >> n;
        string s;
        cin >> s;
        int xs = 0, ys = 0;
        for (auto x : s)
        {
            if (x == 'U')
                ys++;
            if (x == 'D')
                ys--;
            if (x == 'L')
                xs--;
            if (x == 'R')
                xs++;
            if (ys == 1 && xs == 1)
            {
                cout << "YES\n";
                return;
            }
        }
        cout << "NO\n";
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>C. Prepend and Append</font>

  * ### <font size=4 face=粗体>题意</font>

    >Timur initially had a binary string† s(possibly of length 0). He performed the following operation several (possibly zero) times:
    >Add 0to one end of the string and 1to the other end of the string. For example, starting from the string 1011, you can obtain either 010111or 110110.
    >You are given Timur's final string. What is the length of the shortest possible string he could have started with?†A binary string is a string (possibly the empty string) whose characters are either 0or 1.

  * ### <font size=4 face=粗体>思路</font>

    模拟即可，两种选择，删到不能再删为止

  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    /*
    * @Author: NEFU AB-IN
    * @Date: 2023-02-03 22:35:26
    * @FilePath: \CF\1791\c\c.cpp
    * @LastEditTime: 2023-02-03 22:46:12
    */
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #undef int

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 1e5 + 10, INF = 0x3f3f3f3f;

    void solve()
    {
        int n;
        cin >> n;
        string s;
        cin >> s;
        int ans = n;
        for (int i = 0; i < SZ(s); ++i)
        {
            if (ans == 0)
                break;
            if (s[i] == '0' && s[SZ(s) - i - 1] == '1')
                ans -= 2;
            else if (s[i] == '1' && s[SZ(s) - i - 1] == '0')
                ans -= 2;
            else
            {
                cout << ans << '\n';
                return;
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
            solve();
        return 0;
    }

    ```

* ## <font color=#FFA500 size=5>D. Distinct Split</font>

  * ### <font size=4 face=粗体>题意</font>

    >Let's denote the f(x)function for a string xas the number of distinct characters that the string contains. For example f(abc)=3, f(bbbbb)=1, and f(babacaba)=3.
    >Given a string s, split it into two non-empty strings aand bsuch that f(a)+f(b)is the maximum possible. In other words, find the maximum possible value of f(a)+f(b)such that a+b=s(the concatenation of string aand string bis equal to string s).

  * ### <font size=4 face=粗体>思路</font>

    注意这里分字符串，是两者必须连着，也就是两个**子串**
    所以可以预处理到每个点的元素种类，从前往后，从后往前，都处理一遍，最后遍历求最值即可


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #undef int

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 1e5 + 10, INF = 0x3f3f3f3f;

    void solve()
    {
        int n;
        cin >> n;
        string s;
        cin >> s;

        s = '0' + s;
        unordered_map<char, int> st;
        vector<int> a(n + 10), b(n + 10);
        for (int i = 1; i < SZ(s); ++i)
        {
            if (!st.count(s[i]))
                a[i]++;
            st[s[i]]++;
        }
        for (int i = 1; i < SZ(s); ++i)
        {
            a[i] += a[i - 1];
        }
        st.clear();
        for (int i = SZ(s) - 1; i >= 1; --i)
        {
            if (!st.count(s[i]))
                b[i]++;
            st[s[i]]++;
        }
        for (int i = SZ(s) - 1; i >= 1; --i)
        {
            b[i] += b[i + 1];
        }

        int mx = 0;
        for (int i = 1; i + 1 < SZ(s); ++i)
        {
            int ans = a[i] + b[i + 1];
            mx = max(ans, mx);
        }
        cout << mx << '\n';

        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>E. Negatives and Positives</font>

  * ### <font size=4 face=粗体>题意</font>

    >翻译：可以翻转相邻的两个元素的正负，也就是index isuch that 1≤i≤n−1 and assign a[i]=−a[i] and a[i+1]=−a[i+1]
    >问数组最大值

  * ### <font size=4 face=粗体>思路</font>

    两种思路
    * **思维**
      性质：可以发现，翻转**相邻**两元素正负，如果不限制次数，其实也就相当于，数组中两个**任意元素**翻转正负
      那么就考虑**非正数**个数的奇偶性即可
        * 如果是偶数，那么内部消化
        * 如果是奇数，绝对值最小的那个负数不翻转即可

    * **线性dp**
      如果没发现我上面说的**性质**的话，可以采用dp直接推
      我们这里规定：**从下标为2开始，i和i-1同时翻转**
      * **状态表示**：
        * `dp[i][0]`代表到i处的最大值，此时i和i-1不翻转
        * `dp[i][1]`代表到i处的最大值，此时i和i-1翻转
        * **此时i和i-1都必须具有可主动翻转的能力！！**，也就是i-1也可策动i-2翻转，所以，**i必须大于2**
        * 所以我们需要预处理`i=1`和`i=2`的情况
      
      * **状态方程**
        * $$
          dp[i][0] = a[i] + max(dp[i - 1][0], dp[i - 1][1]);
        $$
        * $$
          dp[i][1] = -a[i] + max(dp[i - 1][0] - 2 * a[i - 1], dp[i - 1][1] + 2 * a[i - 1]);
        $$
        * 第二个方程解释一下，就是这个是a[i]翻的情况，那么由于dp[i-1][0]的情况是a[i-1]不翻的最大值，那么此时a[i]翻了，就会策动a[i-1]翻，所以要**减去两倍的a[i-1]**，后面同理

      * 最后输出变或不变的最大值即可

  * ### <font size=4 face=粗体>代码</font>

    **思维**
    ```cpp
    /*
    * @Author: NEFU AB-IN
    * @Date: 2023-02-04 14:02:33
    * @FilePath: \CF\1791\e\e1.cpp
    * @LastEditTime: 2023-02-04 14:28:27
    */
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 2e5 + 10, INF = 0x3f3f3f3f;

    void solve()
    {
        int n, sum = 0, neg = 0;
        cin >> n;
        vector<int> a(n);
        for (int i = 0; i < n; ++i)
        {
            cin >> a[i];
            if (a[i] < 0)
            {
                neg++;
                a[i] = -a[i];
            }
            sum += a[i];
        }
        if (neg % 2)
        {
            int mn = *min_element(ALL(a));
            sum -= 2 * mn;
        }
        cout << sum << '\n';

        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

    ****
    **线性dp**
    ```cpp
    /*
    * @Author: NEFU AB-IN
    * @Date: 2023-02-03 22:35:26
    * @FilePath: \CF\1791\e\e.cpp
    * @LastEditTime: 2023-02-04 11:07:18
    */
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 2e5 + 10, INF = 0x3f3f3f3f;

    int dp[N][2], a[N];

    void solve()
    {
        memset(a, 0, sizeof a);
        memset(dp, 0, sizeof dp);
        int n;
        cin >> n;
        for (int i = 1; i <= n; ++i)
        {
            cin >> a[i];
        }

        dp[1][0] = a[1], dp[1][1] = -a[1];
        dp[2][0] = a[1] + a[2], dp[2][1] = -a[1] - a[2];
        for (int i = 3; i <= n; ++i)
        {
            dp[i][0] = a[i] + max(dp[i - 1][0], dp[i - 1][1]);
            dp[i][1] = -a[i] + max(dp[i - 1][0] - 2 * a[i - 1], dp[i - 1][1] + 2 * a[i - 1]);
        }

        cout << max(dp[n][0], dp[n][1]) << '\n';
        return;
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>F. Range Update Point Query</font>

  * ### <font size=4 face=粗体>题意</font>

    >题意：有一个长度为n的数组a, f函数操作为将a[i] 转换为 a[i]每一位的数的和
    > 1 l r: 代表数组中[l, r]中的所有数都进行一次f操作
    > 2 x  : 代表输出a[x]

  * ### <font size=4 face=粗体>思路</font>

    此题是好题，可以好好记录一下，和**2023牛客寒假训练营第一场的G**一样的思路
    可以采用DSU，线段树等，这里介绍一个set做法

    其实可以观察到这个f函数，梯度下降很快，由于数值最大只有1e9，最大的数就是 99999999->72->9，所以最多变两次，之后变成定值，就不会再变了
    那么思路就是
      * 现将所有**不是定值**的数的**下标**加入set
      * 当出现1操作，即修改时，首先二分找到比l大于等于的第一个下标 (因为可能[l, r]中已经有数是定值，被移出set了)，将其进行f操作并更新回原数组，如果它已经是定值了，则将其移出set。继续根据这个的下标往后找，直到下标超过r，就break
      * 当出现2操作，直接输出a中的值即可


  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long
    #undef int

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 2e5 + 10, INF = 0x3f3f3f3f;

    int f(int x)
    {
        int ans = 0;
        while (x)
        {
            ans += x % 10;
            x /= 10;
        }
        return ans;
    }
    int a[N];

    void solve()
    {
        int n, m;
        cin >> n >> m;
        set<int> st;
        for (int i = 1; i <= n; i++)
        {
            cin >> a[i];
            if (f(a[i]) != a[i])
                st.insert(i);
        }
        st.insert(n + 1);
        for (int i = 1; i <= m; i++)
        {
            int op;
            cin >> op;
            if (op == 1)
            {
                int l, r;
                cin >> l >> r;
                int val = l;
                while (1)
                {
                    auto t1 = st.lower_bound(val);
                    int pos = *t1;
                    if (pos > r)
                        break;
                    a[pos] = f(a[pos]);
                    if (f(a[pos]) == a[pos])
                        st.erase(pos);
                    val = pos + 1;
                }
            }
            else
            {
                int pos;
                cin >> pos;
                cout << a[pos] << '\n';
            }
        }
    }

    signed main()
    {
        IOS;
        int T;
        cin >> T;
        while (T--)
            solve();
        return 0;
    }
    ```

* ## <font color=#FFA500 size=5>G1. Teleporters (Easy Version)</font>

  * ### <font size=4 face=粗体>题意</font>

    >题意：有0,1,...n个地点，其中1到n处有传送门，现在有m个金币，往左往右走会耗费一个金币，走到第i个传送门，如果该处的传送门还存在的话，那么就可以做这个传送门回0（即原点）并花费此处的金币，这个传送门就不可以再用了
    >求用传送门的最多次数

  * ### <font size=4 face=粗体>思路</font>

    其实就是个典型的贪心，类似于背包，总体积为m，物体体积为**金币+下标**，价值为**1**
    由于价值都是一样的，所以**一定是体积越小越好**，所以直接贪即可

    之前一直想的是01背包，还写了01背包的逆过程，结果就是浪费时间...

  * ### <font size=4 face=粗体>代码</font>

    ```cpp
    #include <bits/stdc++.h>
    using namespace std;
    #define int long long

    #define SZ(X) ((int)(X).size())
    #define ALL(X) (X).begin(), (X).end()
    #define IOS                                                                                                            \
        ios::sync_with_stdio(false);                                                                                       \
        cin.tie(nullptr);                                                                                                  \
        cout.tie(nullptr)
    #define DEBUG(X) cout << #X << ": " << X << '\n'
    typedef pair<int, int> PII;

    const int N = 2e5 + 10, INF = 0x3f3f3f3f;

    int dp[N], v[N], V;

    void solve()
    {
        int n;
        cin >> n >> V;
        for (int i = 1; i <= n; ++i)
        {
            cin >> v[i];
            v[i] += i;
        }

        sort(v + 1, v + n + 1);
        int ans = 0;
        for (int i = 1; i <= n; ++i)
        {
            if (V >= v[i])
            {
                V -= v[i];
                ans++;
            }
            else
                break;
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
            solve();
        return 0;
    }
    ```