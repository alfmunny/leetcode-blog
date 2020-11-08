+++
title = "37 - Sudoku Solver"
date = 2020-07-10T17:10:00+02:00
lastmod = 2020-07-10T17:12:10+02:00
tags = ["hard", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/sudoku-solver/)


## Problem {#problem}

```text
Write a program to solve a Sudoku puzzle by filling the empty cells.

A sudoku solution must satisfy all of the following rules:

Each of the digits 1-9 must occur exactly once in each row.
Each of the digits 1-9 must occur exactly once in each column.
Each of the the digits 1-9 must occur exactly once in each of the 9 3x3 sub-boxes of the grid.
Empty cells are indicated by the character '.'.

Note:

The given board contain only digits 1-9 and the character '.'.
You may assume that the given Sudoku puzzle will have a single unique solution.
The given board size is always 9x9.
```


## Solution {#solution}

```python
class Solution:
    def solveSudoku(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        self.finish = False
        self.solve(board, 0, 0)

    def solve(self, board, i, j):
        if i >= len(board):
            self.finish = True
            return
        next_i, next_j = i + (j + 1) // 9, (j + 1) % 9
        if board[i][j] == '.':
            for n in range(1, 10):
                if self.is_safe(board, i, j, str(n)):
                    board[i][j] = str(n)
                    self.solve(board, next_i, next_j)
                    if self.finish:
                        return
                    board[i][j] = '.'
        else:
            self.solve(board, next_i, next_j)

    def is_safe(self, board, i, j, n):
        return self.is_safe_vertical(
            board, i, j, n) and self.is_safe_horizontal(
                board, i, j, n) and self.is_safe_sub(board, i, j, n)

    def is_safe_vertical(self, board, i, j, n):
        return n not in [a[j] for a in board]

    def is_safe_horizontal(self, board, i, j, n):
        return n not in board[i]

    def is_safe_sub(self, board, i, j, n):
        p1 = i // 3 * 3
        p2 = j // 3 * 3
        for x in range(p1, p1 + 3):
            for y in range(p2, p2 + 3):
                if board[x][y] == n:
                    return False
        return True
```
