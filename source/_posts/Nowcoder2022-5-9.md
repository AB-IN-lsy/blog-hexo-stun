---
title: Nowcoder B. 找山坡
tags:
  - Nowcoder
  - 单调栈
  - 树状数组
  - 线段树
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
date: 2022-05-09 15:09:54
---


{% note info %}
**摘要**
Title: Nowcoder B. 找山坡
Tag: 单调栈、树状数组、线段树
Memory Limit: 64 MB
Time Limit: 3000 ms
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>

<font color=#FFA500 size=5 face=楷体>[Link](https://ac.nowcoder.com/acm/contest/34349/B)</font>

@[TOC](文章目录)

# <font color=#6495ED size=6>Nowcoder B. 找山坡</font>

* ## <font size=4 face=粗体>题意</font>

  >母牛哥在电脑面前坐久了，想站起来看看窗外的小山坡，于是就想出了这个问题：
  >给定一个大小为n的数组a，序号从1开始，
  >计算:
  >max{ R - L | 1 <= L <= R <= n, a[L] == a[R], 对于所有i (L <= i <= R), 满足a[i] >= a[L] }.
  >也就是找到两个坐标,这两个坐标的值相等,并且他们之间的值都大于等于这两个坐标上的值.
  >这两个坐标相减最大能是多少.

* ## <font size=4 face=粗体>思路</font>

  题目解析：**找到值相同的两个数，满足两数之间的数都大于等于这两个数，求两数最远隔多远**

  * **思路1 树状数组**
    这是我最一开始的思路，非常麻烦，可以概括为 `树状数组+离散化+双指针`
    * 首先，我们可以观察到，如果**这两个数前面大于等于他们的数之差 恰好等于 他们之间的下标距离**，说明这是符合的一对（因为这就说明了这两个数中间的所有数都大于等于他们），这一点可以仿照树状数组求逆序对来求
    * 其次，上面的等式可以稍做优化，记下每个值的 **k = (前面大于等于他们的数 - 下标)**，为每个值开辟一个vector，把是这个值的 `k` 和 `下标` 记下来
    * 之后，对于每个值的vector进行升序排序，遇到相等的k，就更新结果，和此下标之差取最大值即可，这个操作用双指针即可完成
    * **注意！**
      * `a[i]`的范围，存在0，所以要+1；最大1e9，所以要离散化
  * **思路2 单调栈**
    其实一眼就是单调栈的板子题，每次把大于等于它的数加入进去，如果带进入的数比栈顶小，那么就弹出栈，直到大于等于时，如果此时**栈顶和带进入的数相等了**，说明找到一对，更新最大值即可
    （策略是正确的，因为每次处理离的最近的，保证每对符合要求都能处理到）
  * **思路3 线段树**
    线段树板子题，**维护区间最小值**即可，采用链表跳转到相等的值，判断两者中间的区间最小值和其值的关系，代码就不实现了



* ## <font size=4 face=粗体>代码</font>

  * **思路1 树状数组**

    ```cpp
    #include <bits/stdc++.h>
    using namespace std;

    #define int long long
    #define lowbit(x) x & -x
    #define SZ(X) ((int)X.size())
    const int N = 1e6 + 10;
    int tr[N];
    const int INF = 0x3f3f3f3f;
    typedef pair<int, int> PII;

    void add(int x)
    {
        for (int i = x; i < N; i += lowbit(i))
        {
            tr[i] += 1;
        }
    }
    int query(int x)
    {
        int res = 0;
        for (int i = x; i; i -= lowbit(i))
        {
            res += tr[i];
        }
        return res;
    }
    vector <PII> g[N];
    vector<int> alls = {-INF}; // 存储所有待离散化的值
    signed main()
    {
        int n;
        scanf("%lld", &n);
        vector<int> a(n + 1);
        for (int i = 1; i <= n; ++i)
        {
            scanf("%lld", &a[i]);
            a[i]++;
            alls.push_back(a[i]);
        }
        // 离散化
        sort(alls.begin(), alls.end()); // 将所有值排序
        alls.erase(unique(alls.begin(), alls.end()), alls.end());   // 去掉重复元素
        
        for (int i = 1; i <= n; ++i)
        {
            int id = lower_bound(alls.begin(), alls.end(), a[i]) - alls.begin();
            add(id);
            int num = (i - query(id - 1)); // 查询比它大于等于的数
            g[id].push_back({num - i, i});
        }
        
        int ans = 0;
        for (auto lst : g) // 遍历每个数值的vector
        {
            sort(lst.begin(), lst.end());
            int l = 0, r = 0;
            while (l <= r && l < SZ(lst))
            {
                while (r < SZ(lst) && lst[l].first == lst[r].first)
                    r++;
                ans = max(ans, lst[r - 1].second - lst[l].second);
                l = r;
            }
        }
        printf("%lld\n", ans);
        return 0;
    }
    ```

    ****

  * **思路2 单调栈**

    ```cpp
    #include <bits/stdc++.h>

    using namespace std;
    #define int long long
    #define SZ(X) ((int)X.size())
    typedef pair<int, int> PII;

    signed main()
    {
        int n;
        scanf("%lld", &n);
        vector<int> a(n + 1);
        for (int i = 1; i <= n; ++i)
            scanf("%lld", &a[i]);

        int ans = 0;
        stack<PII> s; // first 值 second 下标
        for (int i = 1; i <= n; ++i)
        {
            while (SZ(s) && s.top().first > a[i])
                s.pop();
            if (SZ(s) && s.top().first == a[i])
                ans = max(ans, i - s.top().second);
            else s.push({a[i], i});
        }
        cout << ans;
        return 0;
    }
    ```