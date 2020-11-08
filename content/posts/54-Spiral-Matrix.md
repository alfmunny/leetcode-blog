+++
title = "54 - Spiral Matrix"
lastmod = 2020-06-18T13:34:19+02:00
categories = ["leetcode"]
draft = true
+++

[leetcode](https://leetcode.com/problems/spiral-matrix/)


## Problem {#problem}

```text
Given a matrix of m x n elements (m rows, n columns), return all elements of the matrix in spiral order.

Example 1:

Input:
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
Output: [1,2,3,6,9,8,7,4,5]
Example 2:

Input:
[
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9,10,11,12]
]
Output: [1,2,3,4,8,12,11,10,9,5,6,7]
```


## Solution {#solution}

```python
class Solution:
    def spiralOrder(self, matrix: List[List[int]]) -> List[int]:
        if not matrix:
            return []
        i = j = 0
        m = len(matrix)
        n = len(matrix[0])
        marked = [[False] * n for _ in matrix]
        step = [[0, 1], [1, 0], [0, -1], [-1, 0]]
        i = j = di = 0
        ans = []
        for _ in range(m*n):
            ans.append(matrix[i][j])
            marked[i][j] = True
            ni, nj = i + step[di][0], j + step[di][1]

            if 0 <= ni < m and 0 <= nj < n and not marked[ni][nj]:
                i, j = ni, nj
            else:
                di = (di + 1) % 4
                i, j = i+step[di][0], j + step[di][1]

        return ans
```
