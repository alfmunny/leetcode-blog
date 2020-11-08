+++
title = "887 - Super Egg Drop"
date = 2020-05-03T01:16:00+02:00
lastmod = 2020-05-03T01:18:43+02:00
tags = ["hard", "dp", "bs", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/super-egg-drop/)


## Problem {#problem}

```text
You are given K eggs, and you have access to a building with N floors from 1 to N.

Each egg is identical in function, and if an egg breaks, you cannot drop it again.

You know that there exists a floor F with 0 <= F <= N such that any egg dropped at a floor higher than F will break, and any egg dropped at or below floor F will not break.

Each move, you may take an egg (if you have an unbroken one) and drop it from any floor X (with 1 <= X <= N).

Your goal is to know with certainty what the value of F is.

What is the minimum number of moves that you need to know with certainty what F is, regardless of the initial value of F?

Example 1:

Input: K = 1, N = 2

Output: 2

Explanation:
Drop the egg from floor 1.  If it breaks, we know with certainty that F = 0.
Otherwise, drop the egg from floor 2.  If it breaks, we know with certainty that F = 1.
If it didn't break, then we know with certainty F = 2.
Hence, we needed 2 moves in the worst case to know what F is with certainty.

Example 2:

Input: K = 2, N = 6

Output: 3

Example 3:

Input: K = 3, N = 14

Output: 4
```


## Solution {#solution}


### Solution 1: dp {#solution-1-dp}

A naive approach with dp. Time consuming.

```python
class Solution:
    def superEggDrop(self, K: int, N: int) -> int:
        memo = dict()

        def dp(K, N):
            if K == 1:
                return N
            if N == 0:
                return 0
            if (K, N) in memo:
                return memo[(K, N)]

            res = float('INF')

            for i in range(1, N+1):
                res = min(res, max(dp(K-1, i-1), dp(K, N - i)) + 1)

            memo[(K, N)] = res
            return res

        return dp(K, N)
```

Time: O(K\*N\*N)

Space: O(K\*N)


### Solution 2: dp with binary search {#solution-2-dp-with-binary-search}

Improve the previous one with a binary search

```python
class Solution:
    def superEggDrop(self, K: int, N: int) -> int:
        memo = dict()

        def dp(K, N):
            if K == 1:
                return N
            if N == 0:
                return 0
            if (K, N) in memo:
                return memo[(K, N)]

            res = float('INF')
            lo = 1
            hi = N
            while lo <= hi:
                mid = (lo + hi) // 2
                broken = dp(K - 1, mid - 1)
                not_broken = dp(K, N - mid)
                if broken > not_broken:
                    hi = mid - 1
                    res = min(res, broken + 1)
                else:
                    lo = mid + 1
                    res = min(res, not_broken + 1)

            memo[(K, N)] = res
            return res

        return dp(K, N)
print(Solution().superEggDrop(3, 14))
```

Time: O(K\*N\*logN)

Space: O(K\*N)


### Solution 3: dp with moves\*eggs {#solution-3-dp-with-moves-eggs}

Use a different transition.

Think about the problem as, given K eggs and M moves, what N can you at least reach.

```python
class Solution:
    def superEggDrop(self, K, N):
      dp = [[0]*(K+1) for _ in range(N+1)]
      m = 0
      while dp[m][K] < N:
          m += 1
          for i in range(1, K+1):
              dp[m][i] = dp[m-1][i] + dp[m-1][i-1] + 1
      return m

print(Solution().superEggDrop(2, 6))
print(Solution().superEggDrop(3, 14))
```

Time: O(K\*N)

Space: O(K\*N)

The transition is only related two previous value, we can reduce the dp matrix two O(1).

```python
class Solution:
    def superEggDrop(self, K, N):
      m = 0
      dp = [0] * (K+1)
      while dp[K] < N:
          m += 1
          prev = 0
          for i in range(1, K+1):
              tmp = dp[i]
              dp[i] = dp[i] + prev + 1
              prev = tmp
      return m
```
