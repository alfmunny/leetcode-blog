+++
title = "980 - Unique Paths III"
date = 2020-08-27T13:21:00+02:00
lastmod = 2020-08-27T13:22:43+02:00
tags = ["hard", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/unique-paths-iii/)


## Problem {#problem}

```text
On a 2-dimensional grid, there are 4 types of squares:

1 represents the starting square.  There is exactly one starting square.
2 represents the ending square.  There is exactly one ending square.
0 represents empty squares we can walk over.
-1 represents obstacles that we cannot walk over.
Return the number of 4-directional walks from the starting square to the ending square, that walk over every non-obstacle square exactly once.



Example 1:

Input: [[1,0,0,0],[0,0,0,0],[0,0,2,-1]]
Output: 2
Explanation: We have the following two paths:
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2)
2. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2)
Example 2:

Input: [[1,0,0,0],[0,0,0,0],[0,0,0,2]]
Output: 4
Explanation: We have the following four paths:
1. (0,0),(0,1),(0,2),(0,3),(1,3),(1,2),(1,1),(1,0),(2,0),(2,1),(2,2),(2,3)
2. (0,0),(0,1),(1,1),(1,0),(2,0),(2,1),(2,2),(1,2),(0,2),(0,3),(1,3),(2,3)
3. (0,0),(1,0),(2,0),(2,1),(2,2),(1,2),(1,1),(0,1),(0,2),(0,3),(1,3),(2,3)
4. (0,0),(1,0),(2,0),(2,1),(1,1),(0,1),(0,2),(0,3),(1,3),(1,2),(2,2),(2,3)
Example 3:

Input: [[0,1],[2,0]]
Output: 0
Explanation:
There is no path that walks over every empty square exactly once.
Note that the starting and ending square can be anywhere in the grid.


Note:

1 <= grid.length * grid[0].length <= 20
```


## Solution {#solution}

```python
class Solution:
    def uniquePathsIII(self, grid: List[List[int]]) -> int:
        count = len([x for r in grid for x in r if x == 0]) + 2
        start = [[i,j] for i in range(len(grid)) for j in range(len(grid[0])) if grid[i][j] == 1][0]
        self.ans = 0
        self.dfs(grid, start[0], start[1], 0, count)
        return self.ans

    def dfs(self, grid, i, j, curCount, count):

        if i < 0 or i >= len(grid) or j < 0 or j >= len(grid[0]) or grid[i][j] in [-1, 100]:
            return

        if curCount == count-1 and grid[i][j] == 2:
            self.ans += 1
            return
        elif grid[i][j] == 2:
            return

        x = grid[i][j]
        grid[i][j] = 100
        for di, dj in [[0, 1], [0, -1], [1, 0], [-1, 0]]:
            self.dfs(grid, i+di, j+dj, curCount+1, count)

        grid[i][j] = x
```
