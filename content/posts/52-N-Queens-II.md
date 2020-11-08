+++
title = "52 - N-Queens II"
date = 2020-06-12T17:44:00+02:00
lastmod = 2020-06-12T17:45:25+02:00
tags = ["hard", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/n-queens-ii/)


## Problem {#problem}

```text
The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

Given an integer n, return the number of distinct solutions to the n-queens puzzle.
```


## Solution {#solution}

```python
class Solution:
    def totalNQueens(self, n):
        self.ans = 0
        self.dfs(0, n, [])
        return self.ans

    def dfs(self, row, n, path):
        if row == n and len(path) == n:
            self.ans += 1
        for i in range(n):
            if self.attack(path, row, i):
                continue
            path.append([row, i])
            self.dfs(row+1, n, path)
            path.pop()

    def attack(self, path, row, i):
        for pair in path:
            if pair[1] == i:
                return True
            elif abs(row - pair[0]) == abs(i - pair[1]):
                return True
        return False
```
