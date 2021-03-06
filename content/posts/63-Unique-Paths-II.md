+++
title = "63 - Unique Paths II"
date = 2020-06-18T14:25:00+02:00
lastmod = 2020-06-18T14:25:31+02:00
tags = ["medium", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/unique-paths-ii/)


## Problem {#problem}

```text
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?

An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Note: m and n will be at most 100.

Example 1:

Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```


## Solution {#solution}

```python
class Solution:
    def uniquePathsWithObstacles(self, obstacleGrid: List[List[int]]) -> int:
        if not obstacleGrid:
            return 0

        m, n = len(obstacleGrid), len(obstacleGrid[0])

        dp = [[0] * (n+1) for _ in range(m+1)]

        dp[0][1] = 1

        for i in range(m):
            for j in range(n):
                if not obstacleGrid[i][j]:
                    dp[i+1][j+1] = dp[i+1][j] + dp[i][j+1]

        return dp[-1][-1]
```
