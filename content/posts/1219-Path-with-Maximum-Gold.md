+++
title = "1219 - Path with Maximum Gold"
date = 2020-08-23T19:07:00+02:00
lastmod = 2020-08-23T19:08:52+02:00
tags = ["medium", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/path-with-maximum-gold/)


## Problem {#problem}

```text
In a gold mine grid of size m * n, each cell in this mine has an integer representing the amount of gold in that cell, 0 if it is empty.

Return the maximum amount of gold you can collect under the conditions:

Every time you are located in a cell you will collect all the gold in that cell.
From your position you can walk one step to the left, right, up or down.
You can't visit the same cell more than once.
Never visit a cell with 0 gold.
You can start and stop collecting gold from any position in the grid that has some gold.


Example 1:

Input: grid = [[0,6,0],[5,8,7],[0,9,0]]
Output: 24
Explanation:
[[0,6,0],
 [5,8,7],
 [0,9,0]]
Path to get the maximum gold, 9 -> 8 -> 7.
Example 2:

Input: grid = [[1,0,7],[2,0,6],[3,4,5],[0,3,0],[9,0,20]]
Output: 28
Explanation:
[[1,0,7],
 [2,0,6],
 [3,4,5],
 [0,3,0],
 [9,0,20]]
Path to get the maximum gold, 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7.
```


## Solution {#solution}

```python
class Solution:
    def getMaximumGold(self, grid: List[List[int]]) -> int:
        self.ans = 0
        mark = [[False] * len(grid[0]) for _ in grid]

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                self.dfs(grid, i, j, mark, 0)

        return self.ans

    def dfs(self, grid, i, j, mark, gold):

        if i < 0 or i == len(grid) or j < 0 or j == len(grid[0]) or mark[i][j] or not grid[i][j]:
            self.ans = max(self.ans, gold)
            return

        mark[i][j] = True

        for di, dj in [[1,0], [0, 1], [-1, 0], [0, -1]]:
            self.dfs(grid, i+di, j+dj, mark, gold+grid[i][j])

        mark[i][j] = False
```
