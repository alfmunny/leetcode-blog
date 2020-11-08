+++
title = "463 - Island Perimeter"
date = 2020-07-07T16:13:00+02:00
lastmod = 2020-07-07T16:14:53+02:00
tags = ["easy", "array", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/island-perimeter/)


## Problem {#problem}

```text
You are given a map in form of a two-dimensional integer grid where 1 represents land and 0 represents water.

Grid cells are connected horizontally/vertically (not diagonally). The grid is completely surrounded by water, and there is exactly one island (i.e., one or more connected land cells).

The island doesn't have "lakes" (water inside that isn't connected to the water around the island). One cell is a square with side length 1. The grid is rectangular, width and height don't exceed 100. Determine the perimeter of the island.
```


## Solution {#solution}

```python
class Solution:
    def islandPerimeter(self, grid: List[List[int]]) -> int:
        if not grid or not grid[0]:
            return 0

        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j]:
                    return self.dfs(grid, i, j)
        return 0

    def dfs(self, grid, i, j):
        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]):
            return 1

        if grid[i][j] == -1:
            return 0

        if grid[i][j]:
            grid[i][j] = -1
            return self.dfs(grid, i + 1, j) + self.dfs(
                grid, i, j + 1) + self.dfs(grid, i - 1, j) + self.dfs(
                    grid, i, j - 1)
        else:
            return 1
```
