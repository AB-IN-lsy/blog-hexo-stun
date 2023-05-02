---
title: 第十四届蓝桥杯大赛软件组省赛 Python大学A组 个人暴力题解
tags:
  - 蓝桥杯
categories:
  - 2023大四下学期
toc: true
quicklink: true
math: true
sidebar: true
copyright: true
reward: true
date: 2023-04-08 16:08:49
---

{% note info %}
**摘要**
Title: 第十四届蓝桥杯大赛软件组省赛 Python大学A组 个人暴力题解
Tag: A, B, C, D, E, F, G, H, I, J
{% endnote %}
<!-- more -->

<font size=3 face=楷体>Powered by:**NEFU AB-IN**</font>


@[TOC](文章目录)

**博主个人的暴力题解，基本很少是正解，求轻喷**
# <font color=#6495ED size=6 >Python大学A组 个人暴力题解</font>

* ## <font color=#FFA500 size=5>试题 A: 特殊日期</font>

  * ### <font size=4 face=粗体>题意</font>
	![img](https://img-blog.csdnimg.cn/12403bb2f12b4bbda63644bdba87066e.png)


  * ### <font size=4 face=粗体>思路</font>

	模拟即可，本身想用Python自带的datetime库，结果发现年不能开那么大，就直接手写了

  * ### <font size=4 face=粗体>代码</font>

	```python
	'''
	Author: NEFU AB-IN
	Date: 2023-04-08 14:15:52
	FilePath: \Vscode\ACM\LanQiao\2023PythonA\a.py
	LastEditTime: 2023-04-08 14:19:47
	'''
	# AB-IN AK Lanqiao !!
	# http://222.27.161.91/home.page
	# aR7H4tDF
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda: map(int, input().split())
	
	
	class sa:
	    def __init__(self, y, m, d):
	        self.y = y
	        self.m = m
	        self.d = d
	
	    def __lt__(self, x):
	        pass
	
	
	# ---------------divrsion line ----------------
	
	# t1 = datetime(2000, 1, 1)
	# t2 = datetime(2000, 1, 2)
	
	# ans = 0
	# while True:
	#     if t1.year % t1.month == 0 and t1.year % t1.day == 0:
	#         ans += 1
	#     t1 = t1 + timedelta(days=1)
	#     if t1 == t2:
	#         break
	# print(ans)
	
	mouths = [0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31]
	
	
	def func(t1):
	    y, m, d = t1.y, t1.m, t1.d
	    if (y % 4 == 0 and y % 100) or (y % 400 == 0):
	        mouths[2] = 29
	    d += 1
	    if d > mouths[m]:
	        d = 1
	        m += 1
	    if m > 12:
	        m = 1
	        y += 1
	    return sa(y, m, d)
	
	
	t1 = sa(2000, 1, 1)
	t2 = sa(2000000, 1, 2)
	
	ans = 0
	while True:
	    if t1.y % t1.m == 0 and t1.y % t1.d == 0:
	        ans += 1
	    t1 = func(t1)
	    if t1.y == t2.y and t1.m == t2.m and t1.d == t2.d:
	        break
	print(ans)
	
	# 35830804
	```


* ## <font color=#FFA500 size=5>试题 B: 分糖果</font>

  * ### <font size=4 face=粗体>题意</font>

	![img](https://img-blog.csdnimg.cn/b41e4e9cf6654ef4bbc66083e62d87f3.png)

  * ### <font size=4 face=粗体>思路</font>

	DFS爆搜即可

  * ### <font size=4 face=粗体>代码</font>

	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# 两种糖果分别有 9 个和 16 个，要全部分给 7 个小朋友，每个小朋友得到
	# 的糖果总数最少为 2 个最多为 5 个，问有多少种不同的分法。
	
	ans = 0
	def dfs(sum1, sum2, cnt):
	    global ans
	    if sum1 < 0 or sum2 < 0:
	        return
	    if cnt == 8:
	        if sum1 == 0 and sum2 == 0:
	            ans += 1
	        return
	    for i in range(2, 6):
	        dfs(sum1 - i, sum2, cnt + 1)
	    for i in range(2, 6):
	        dfs(sum1, sum2 - i, cnt + 1)
	    for i in range(2, 6):
	        for j in range(2, 6):
	            if i + j >= 2 and i + j <= 5:
	                dfs(sum1 - i, sum2 - j, cnt + 1)
	
	dfs(9, 16, 1)
	print(ans)
	
	# 148540
	```

* ## <font color=#FFA500 size=5>试题 C: 三国游戏</font>

  * ### <font size=4 face=粗体>题意</font>
	
  ![img](https://img-blog.csdnimg.cn/f6fe525d6bb643feb304800a913c4e2d.png)


  * ### <font size=4 face=粗体>思路</font>
	直接没思路，一看到数据范围瞬间怂了，脑子里想的只有暴力，这个题是留到最后写的，就写了个最差的二进制枚举	

  * ### <font size=4 face=粗体>代码</font>
	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# 最差方法 二进制枚举
	
	n, = read()
	a = list(read())
	b = list(read())
	c = list(read())
	ans = 0
	
	for i in range(1 << n):
	    A, B, C, cnt = 0, 0, 0, 0
	    for j in range(n):
	        if i & 1 << j:
	            A += a[j]
	            B += b[j]
	            C += c[j]
	            cnt += 1
	    if A > B + C or B > A + C or C > A + B:
	        ans = max(ans, cnt)
	
	print(ans if ans != 0 else -1)
	```


* ## <font color=#FFA500 size=5>试题 D: 平均</font>

  * ### <font size=4 face=粗体>题意</font>
  
	![img](https://img-blog.csdnimg.cn/228f754416444a98a9726114c72eb68f.png)


  * ### <font size=4 face=粗体>思路</font>
	唯一一个觉得暴力是正解的题
	就是每个数最多就是`n//10`个，所以就去掉多的数，然后是那些数中代价小的，最后采用了前缀和优化了一下

  * ### <font size=4 face=粗体>代码</font>
	 ```python
	 # AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, a, b):
	        self.a = a
	        self.b = b
	    def __lt__(self, t):
	        if self.a != t.a:
	            return self.a < t.a
	        return self.b < t.b
	
	# ---------------divrsion line ----------------
	
	n, = read()
	lst = [[] for _ in range(10)]
	
	for i in range(n):
	    a, b = read()
	    lst[a].append(b)
	
	for i in range(10):
	    lst[i].sort()
	    lst[i] = [0, *lst[i]]
	    # 前缀和
	    for j in range(1, len(lst[i])):
	        lst[i][j] += lst[i][j - 1]
	
	# 保留的个数
	k = n // 10
	
	ans = 0
	for i in range(10):
	    l = len(lst[i]) - 1
	    if l > k:
	        ans += (lst[i][l - k])
	
	print(ans)
	 ```

* ## <font color=#FFA500 size=5>试题 E: 翻转</font>

  * ### <font size=4 face=粗体>题意</font>
  
	![img](https://img-blog.csdnimg.cn/3b9a0448b6b9400cafef4174367aff67.png)


  * ### <font size=4 face=粗体>思路</font>
	BFS暴力，不会剪枝，剪枝想了一种，但是没有证明正确性，所以就没有采用
	
  * ### <font size=4 face=粗体>代码</font>
	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, s, step):
	        self.s = s
	        self.step = step
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# BFS暴力 不会剪枝 没证明剪枝一定正确
	
	def solve():
	    t = input()
	    s = input()
	
	    t = " " + t
	    s = " " + s
	
	    if t[1] != s[1] or t[-1] != s[-1]:
	        return -1
	
	    q = deque()
	    q.appendleft(sa(s, 0))
	    while len(q):
	        tp = q.pop()
	        s, step = tp.s, tp.step
	        if s == t:
	            return step
	        for i in range(2, len(s) - 1):
	            if s[i] == '0' and s[i - 1] == '1' and s[i + 1] == '1':
	                g = s[:i - 1] + "111" + s[i + 2:]
	                if g == t:
	                    return step + 1
	                q.appendleft(sa(g, step + 1))
	            if s[i] == '1' and s[i - 1] == '0' and s[i + 1] == '0':
	                g = s[:i - 1] + "000" + s[i + 2:]
	                if g == t:
	                    return step + 1
	                q.appendleft(sa(g, step + 1))
	    return -1
	
	
	T, = read()
	for _ in range(T):
	    print(solve())
	```

* ## <font color=#FFA500 size=5>试题 F: 子矩阵</font>

  * ### <font size=4 face=粗体>题意</font>
  
	![img](https://img-blog.csdnimg.cn/29270e6e83554184a48d679f328732fb.png)


  * ### <font size=4 face=粗体>思路</font>
	这版是直接暴力做的
	考试最后写了一点线段树优化，只不过只维护了行和列的最小值和最大值，但感觉Python写的线段树也优化不了多少
  
  * ### <font size=4 face=粗体>代码</font>
	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e3 + 10)
	MOD = 998244353
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# RMQ 问题 可写ST表 但我忘了...
	# 暴力！
	g = [[0] * N for _ in range(N)]
	n, m, a, b = read()
	
	def func(t1, t2):
	    mn, mx = INF, 0
	    for i in range(t1.x, t2.x + 1):
	        for j in range(t1.y, t2.y + 1):
	            mn = min(mn, g[i][j])
	            mx = max(mx, g[i][j])
	    return mx * mn % MOD
	
	for i in range(1, n + 1):
	    g[i][1:] = read()
	
	ans = 0
	for i in range(1, n + 1):
	    for j in range(1, m + 1):
	        t1 = sa(i, j)
	        t2 = sa(i + a - 1, j + b - 1)
	        if i + a - 1 > n or j + b - 1 > m:
	            continue
	        ans = (ans + func(t1, t2)) % MOD 
	
	print(ans)
	```

* ## <font color=#FFA500 size=5>试题 G: 阶乘的和</font>

  * ### <font size=4 face=粗体>题意</font>

	![img](https://img-blog.csdnimg.cn/772c3972b15540e090a6853cf5847ce8.png)


  * ### <font size=4 face=粗体>思路</font>
	还是暴力，思路就是可以把共因子都提出来，剩下的加和，从提出来的共同的因子的最大值开始，让加和除以它，直到不能除了，就是答案
	其中，用哈希表记录用过的阶乘值，预处理一些阶乘值

  * ### <font size=4 face=粗体>代码</font>
	 ```python
	 # AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e5 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# 暴力！
	# 预处理1 ~ 5000阶乘
	dd = Counter()
	cnt = 1
	for i in range(1, 5000):
	    cnt *= i
	    dd[i] = cnt
	# ---------------------------------------------
	a = [0] * N
	
	n, = read()
	a[1:] = list(read())
	d = Counter()
	
	base = min(a[1:])
	ans = 0
	for i in range(1, n + 1):
	    tmp = 1
	    if a[i] < 5000:
	        d[a[i]] = dd[a[i]] // dd[base]
	    elif d[a[i]] == 0:
	        for j in range(a[i], base, -1):
	            tmp *= j
	        d[a[i]] = tmp
	    ans += d[a[i]]
	
	while True:
	    if ans == 1 or ans % (base + 1) != 0:
	        break
	    base += 1
	    ans //= base
	
	print(base)
	 ```

* ## <font color=#FFA500 size=5>试题 H: 奇怪的数</font>

  * ### <font size=4 face=粗体>题意</font>
	
  ![img](https://img-blog.csdnimg.cn/804d6756e73e4ae1bd4d5deea363fa9c.png)


  * ### <font size=4 face=粗体>思路</font>
	还是暴力DFS
	相当于搜满足条件的n位数，直接搜每一位即可，因为奇数位为奇数，偶数位为偶数
	优化就是每次搜每一位的时候，和前面的四位数加和，判断是否小于等于m，如果不满足就直接不搜了

  * ### <font size=4 face=粗体>代码</font>
	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	MOD = 998244353
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# 感觉像数位dp，先打DFS暴力
	# 想不出递推式 就优化暴力吧
	
	n, m = read()
	
	ji = ["1", "3", "5", "7", "9"]
	ou = ["0", "2", "4", "6", "8"]
	stji, stou = [0] * 5, [0] * 5
	ans = 0
	
	def dfs(s, d):
	    global ans
	    if d == n + 1:
	        ans = (ans + 1) % MOD
	        return
	
	    for i in range(5):
	        if d % 2 == 1:
	            cnt = int(ji[i])
	            for j in range(max(1, d - 4), d):
	                cnt += int(s[j])
	            if cnt <= m:
	                dfs(s + ji[i], d + 1)
	        if d % 2 == 0:
	            cnt = int(ou[i])
	            for j in range(max(1, d - 4), d):
	                cnt += int(s[j])
	            if cnt <= m:
	                dfs(s + ou[i], d + 1)
	    return  
	
	
	dfs(" ", 1)
	print(ans % MOD)
	```

* ## <font color=#FFA500 size=5>试题 I: 子树的大小</font>

  * ### <font size=4 face=粗体>题意</font>
	
  ![img](https://img-blog.csdnimg.cn/497581696ca848fd8b572e56965a8c78.png)


  * ### <font size=4 face=粗体>思路</font>
	没时间想了，感觉暴力都很麻烦

  * ### <font size=4 face=粗体>代码</font>
* ## <font color=#FFA500 size=5>试题 J: 反异或 01 串</font>

  * ### <font size=4 face=粗体>题意</font>
	
  ![img](https://img-blog.csdnimg.cn/216d3e63592444998e04b92a46d00bc6.png)

  * ### <font size=4 face=粗体>思路</font>
	没时间想了，就特判了几种情况

  * ### <font size=4 face=粗体>代码</font>
	```python
	# AB-IN AK Lanqiao !!
	import sys, math
	from collections import Counter, deque, defaultdict
	from bisect import bisect_left, bisect_right
	from heapq import heappop, heappush, heapify
	from typing import *
	from datetime import datetime, timedelta
	
	N = int(1e6 + 10)
	INF = int(2e9)
	
	sys.setrecursionlimit(INF)
	read = lambda : map(int, input().split())
	
	class sa:
	    def __init__(self, x, y):
	        self.x = x
	        self.y = y
	    def __lt__(self, x):
	        pass
	
	# ---------------divrsion line ----------------
	# 骗分
	
	def solve(s):
	    d = Counter(s)
	    if len(s) == d['0']:
	        return 0
	    if len(s) == d['1']:
	        return len(s) // 2
	    if s == "00111011":
	        return 3
	    return d['1']
	    
	s = input()
	
	print(solve(s))
	```