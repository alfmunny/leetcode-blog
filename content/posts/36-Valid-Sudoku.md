+++
title = "36 - Valid Sudoku"
date = 2020-07-12T23:45:00+02:00
lastmod = 2020-07-12T23:47:11+02:00
tags = ["medium", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/valid-sudoku/)


## Problem {#problem}

```text
Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.
```


## Solution {#solution}

```python
class Solution:
    def isValidSudoku(self, board: List[List[str]]) -> bool:
        for row in board:
            nums = [x for x in row if x != '.' ]
            if self.notValid(nums):
                return False

        for i in range(len(board[0])):
            col = [row[i] for row in board]
            nums = [x for x in col if x != '.' ]
            if self.notValid(nums):
                return False

        for i in [0, 3, 6]:
            for j in [0, 3, 6]:
                nums = [x for row in board[i:i+3] for x in row[j:j+3] if x != '.']
                if self.notValid(nums):
                    return False
        return True

    def notValid(self, nums):
        return len(set(nums)) != len(nums)
```
