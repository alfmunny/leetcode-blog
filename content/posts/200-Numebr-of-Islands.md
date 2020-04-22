+++
title = "200 - Number of Islands"
date = 2020-04-17T17:01:00+02:00
lastmod = 2020-04-17T17:01:58+02:00
tags = ["medium", "array", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/number-of-islands/)


## Problem {#problem}

```text
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:

Input:
11110
11010
11000
00000

Output: 1
Example 2:

Input:
11000
11000
00100
00011

Output: 3
```


## Solution {#solution}

DFS problem. Straight forward.

```python
class Solution:
    def numIslands(self, grid):
        if not grid:
            return 0
        h = len(grid)
        w = len(grid[0])
        ans = 0
        m = [ [0] * w for x in range(h) ]
        for i in range(h):
            for j in range(w):
                if grid[i][j] == "1" and m[i][j] == 0:
                    self.dfs(grid, i, j, m)
                    ans += 1
        return ans

    def dfs(self, grid, i, j, m):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] == "0" or m[i][j] == 1:
            return None
        else:
            m[i][j] = 1
            self.dfs(grid, i, j+1, m)
            self.dfs(grid, i, j-1, m)
            self.dfs(grid, i-1, j, m)
            self.dfs(grid, i+1, j, m)
        return None
```
