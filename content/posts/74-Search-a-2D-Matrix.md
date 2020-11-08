+++
title = "74 - Search a 2D Matrix"
date = 2020-06-18T14:46:00+02:00
lastmod = 2020-06-18T14:47:31+02:00
tags = ["medium", "array", "bs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/search-a-2d-matrix/)


## Problem {#problem}

```text
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:

Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
Example 1:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
Example 2:

Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```


## Solution {#solution}

```python
class Solution:
    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:
        if not matrix or not matrix[0]:
            return False

        rl, rr = 0, len(matrix) - 1
        cl, cr = 0, len(matrix[0]) - 1

        while rl <= rr:
            mid = (rl + rr) // 2
            if target < matrix[mid][0]:
                rr = mid - 1
            elif target > matrix[mid][-1]:
                rl = mid + 1
            else:
                rl = mid
                break

        if rl > rr:
            return False

        while cl <= cr:
            mid = (cl + cr) // 2

            if target < matrix[rl][mid]:
                cr = mid - 1
            elif target > matrix[rl][mid]:
                cl = mid + 1
            else:
                return True

        return False
```
