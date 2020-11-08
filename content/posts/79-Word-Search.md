+++
title = "79 - Word Search"
date = 2020-03-14T03:00:00+01:00
lastmod = 2020-08-24T18:33:55+02:00
tags = ["medium", "array", "backtrack", "dfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/word-search/)


## Problem {#problem}

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

Backtrack problem.

1.  when found, mark the point to one.
2.  Use dfs to go down from this point.
3.  Can't go down anymore, mark the point back to zero (backtrack step).


## Solution {#solution}


### Solution 1: Backtrack, dfs {#solution-1-backtrack-dfs}

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        for i in range(len(board)):
            for j in range(len(board[0])):
                if self.dfs(board, word, 0, i, j):
                    return True
        return False

    def dfs(self, board, word, w, i, j):
        if w == len(word):
            return True

        if i < 0 or j < 0 or i >= len(board) or j >= len(board[0]):
            return False

        if board[i][j] == word[w]:
            board[i][j] = '-'

            for next_i, next_j in [[i + 1, j], [i - 1, j], [i, j - 1],
                                   [i, j + 1]]:
                if self.dfs(board, word, w + 1, next_i, next_j):
                    return True

            board[i][j] = word[w]

        return False
```
