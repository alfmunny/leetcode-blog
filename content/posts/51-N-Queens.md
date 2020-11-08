+++
title = "51 - N-Queens"
date = 2020-06-12T17:38:00+02:00
lastmod = 2020-06-12T17:39:35+02:00
tags = ["hard", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/n-queens/)


## Problem {#problem}

```text
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens' placement, where 'Q' and '.' both indicate a queen and an empty space respectively.
```


## Solution {#solution}

```python
class Solution:
    def solveNQueens(self, n):
        ans = []

        self.dfs(0, n, [], ans)
        return ans

    def dfs(self, row, n, path, ans):
        if row == n and len(path) == n:
            ans.append(self.draw(path, n))
        for i in range(n):
            if self.attack(path, row, i):
                continue
            path.append([row, i])
            self.dfs(row+1, n, path, ans)
            path.pop()

    def attack(self, path, row, i):
        for pair in path:
            if pair[1] == i:
                return True
            elif abs(row - pair[0]) == abs(i - pair[1]):
                return True
        return False

    def draw(self, path, n):
        ans = []
        for pair in path:
            ans.append("." * pair[1] + "Q" + "." * (n-1-pair[1]))

        return ans
```
