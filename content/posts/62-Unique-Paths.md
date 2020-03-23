+++
title = "62 - Unique Paths"
author = ["alfmunny"]
lastmod = 2020-03-21T22:34:22+01:00
tags = ["medium", "array", "dp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/unique-paths/)


## Problem {#problem}

```text
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?

Note: m and n will be at most 100.

Example 1:

Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
Example 2:

Input: m = 7, n = 3
Output: 28
```


## Notes {#notes}

It is a DP problem.

1.  There are only two possibilities to arrive at the finish point
    1.  arrive at that point from above
    2.  arrive at that point from left

2.  So the ways to arrive at current point is equal to the ways from above plus the ways from left. dp[i][j] = dp[i][j-1] + dp[i - 1][j]
3.  Dynamic programming. Maintain a two dimensional matrix.
4.  Optimize it to one dimension.
5.  Complexity O(m \* n)


### UniquePath with 2-D DP {#uniquepath-with-2-d-dp}

```python
dp[i][j] = dp[i-1][j] + dp[i][j-1]
```

After you have the edge, you go levelly to the bottom.


### UniquePath with 1-D DP {#uniquepath-with-1-d-dp}

```python
dp[j] = dp[j - 1] + dp[j]
```


## Solution {#solution}


### Solution 1: 2-D DP {#solution-1-2-d-dp}

```python
class Solution():
    def uniquePath(self, m, n):
        dp = [[1 for j in range(n)] for i in range(m)]
        for i in range(1, m):
            for j in range(1, n):
                dp[i][j] = dp[i][j - 1] + dp[i - 1][j]

        return dp[-1][-1] if m and n else 0
```


### Solution 2: 1-D DP {#solution-2-1-d-dp}

```python
class Solution():
    def uniquePath(self, m, n):
        dp = [1] * n

        for i in range(1, m):
            for j in range(1, n):
                dp[j] = dp[j - 1] + dp[j]

        return dp[-1] if m and n else 0
```
