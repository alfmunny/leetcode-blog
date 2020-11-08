+++
title = "1277 - Count Square Submatrices with All Ones"
date = 2020-05-22T00:01:00+02:00
lastmod = 2020-05-22T00:02:37+02:00
tags = ["medium", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/count-square-submatrices-with-all-ones/)


## Problem {#problem}

```text
Given a m * n matrix of ones and zeros, return how many square submatrices have all ones.



Example 1:

Input: matrix =
[
  [0,1,1,1],
  [1,1,1,1],
  [0,1,1,1]
]
Output: 15
Explanation:
There are 10 squares of side 1.
There are 4 squares of side 2.
There is  1 square of side 3.
Total number of squares = 10 + 4 + 1 = 15.

Example 2:

Input: matrix =
[
  [1,0,1],
  [1,1,0],
  [1,1,0]
]
Output: 7
Explanation:
There are 6 squares of side 1.
There is 1 square of side 2.
Total number of squares = 6 + 1 = 7.
```


## Solution {#solution}

DP problem. Same as p227.

```python
class Solution:
    def countSquares(self, matrix):
        if not matrix or not matrix[0]:
            return 0
        m = len(matrix)
        n = len(matrix[0])
        ans = 0
        for i in range(m):
            for j in range(n):
                if matrix[i][j] == 1:
                    if i and j:
                        matrix[i][j] = min(matrix[i-1][j-1], matrix[i][j-1], matrix[i-1][j]) + 1
                    ans += matrix[i][j]
        return ans
```
