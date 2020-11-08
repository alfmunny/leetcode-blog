+++
title = "240 - Search a 2D Matrix II"
date = 2020-08-17T03:11:00+02:00
lastmod = 2020-08-17T16:42:04+02:00
tags = ["medium", "array", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/search-a-2d-matrix-ii/)


## Problem {#problem}

```text
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted in ascending from left to right.
Integers in each column are sorted in ascending from top to bottom.

Example:

Consider the following matrix:

[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
Given target = 5, return true.

Given target = 20, return false.
```


## Solution {#solution}


### Solution 1 {#solution-1}

```python
class Solution:
    def searchMatrix(self, matrix, target):
        """
        :type matrix: List[List[int]]
        :type target: int
        :rtype: bool
        """
        if not matrix or not matrix[0]:
            return False

        j = 0

        for row in matrix:
            if row[j] > target:
                while row[j] > target:
                    j -= 1
                    if j < 0:
                        return False


            elif row[j] < target:
                while row[j] < target:
                    j += 1
                    if j == len(matrix[0]):
                        j = 0
                        break


            if row[j] == target:
                return True

        return False
```


### Solution 2: Like a binary tree {#solution-2-like-a-binary-tree}

Start from upper right corner.

If matrix[i][j] > target: col - 1

if matrix[i][j] < target: row + 1

```python
class Solution:
    def searchMatrix(self, matrix, target):
        if not matrix or not matrix[0]:
            return False

        i, j = 0, len(matrix[0]) - 1
        while i < len(matrix) and j >= 0 :

            if matrix[i][j] == target:
                return True
            elif matrix[i][j] > target:
                j -= 1
            else:
                i += 1
        return False
```
