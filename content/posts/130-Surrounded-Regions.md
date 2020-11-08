+++
title = "130 - Surrounded Regions"
date = 2020-06-26T01:58:00+02:00
lastmod = 2020-06-26T01:59:40+02:00
tags = ["medium", "array", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/explore/featured/card/june-leetcoding-challenge/541/week-3-june-15th-june-21st/3363/)


## Problem {#problem}

```text
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:

X X X X
X O O X
X X O X
X O X X
After running your function, the board should be:

X X X X
X X X X
X X X X
X O X X
Explanation:

Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
```


## Solution {#solution}

```python
class Solution:
    def solve(self, board: List[List[str]]) -> None:
        """
        Do not return anything, modify board in-place instead.
        """
        if not board or not board[0]:
            return

        marked = [[False] * len(board[0]) for _ in board]

        for i in range(len(board)):
            for j in range(len(board[0])):
                self.flag = False
                if board[i][j] == 'O' and not marked[i][j]:
                    self.dfs(i, j, board, marked)

                    if not self.flag:
                        self.color(i, j, board)

    def dfs(self, i, j, board, marked):
        marked[i][j] = True

        for x, y in [(i + 1, j), (i - 1, j), (i, j + 1), (i, j - 1)]:
            if x < 0 or x >= len(board) or y < 0 or y >= len(board[0]):
                self.flag = True
                continue

            if marked[x][y]:
                continue

            if board[x][y] == 'O':
                self.dfs(x, y, board, marked)

    def color(self, i, j, board):
        board[i][j] = 'X'
        for x, y in [(i + 1, j), (i - 1, j), (i, j + 1), (i, j - 1)]:
            if board[x][y] == 'O':
                self.color(x, y, board)
```
