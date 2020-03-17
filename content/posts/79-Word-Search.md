+++
title = "79 - Word Search"
author = ["alfmunny"]
date = 2020-03-14T03:00:00+01:00
lastmod = 2020-03-14T10:17:59+01:00
tags = ["medium", "array", "backtrack"]
categories = ["leetcode"]
draft = false
+++

## Problem {#problem}

[leetcode](https://leetcode.com/problems/word-search/)

```text
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

Example:

board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```


## Notes {#notes}


## Solution {#solution}


### Solution 1: Backtrack {#solution-1-backtrack}

```python
class Solution:
    def exist(self, board, word):
        m = [[0 for j in range(len(board[0]))] for i in range(len(board))]
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.exist_rec(board, word, i, j, m):
                    return True
        return False

    def exist_rec(self, board, word, i, j, m):
        if len(word) == 0:
            return True

        if i < 0 or j < 0 or i >= len(board) or j >= len(board[0]):
            return False

        if board[i][j] == word[0] and m[i][j] == 0:
            m[i][j] = 1

            if self.exist_rec(board, word[1:], i - 1, j, m) or \
            self.exist_rec(board, word[1:], i + 1, j, m) or \
            self.exist_rec(board, word[1:], i, j - 1, m) or \
            self.exist_rec(board, word[1:], i, j + 1, m):
                return True
            else:
                m[i][j] = 0

        return False

board = [["A", "B", "C", "E"], ["S", "F", "C", "S"], ["A", "D", "E", "E"]]
word = "ABCCED"
```
