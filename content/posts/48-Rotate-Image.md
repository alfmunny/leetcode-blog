+++
title = "48 - Rotate Image"
author = ["alfmunny"]
lastmod = 2020-03-21T22:16:23+01:00
tags = ["medium", "array", "constant-memory"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/rotate-image/)


## Problem {#problem}

```text
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

Given input matrix =
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
Example 2:

Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
],

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
```


## Notes {#notes}


### Naive solution, to do it one by one. {#naive-solution-to-do-it-one-by-one-dot}

**Important**:

You go from the outside into the middle. So the main loop is half of the dimension.

The inner loop should also shrink its size everytime. Begins at i and ends and n-2-i, **not n-1-i**.

Because you don't want to swap the last one. The last one n-1-i has already been swapped with the i.


### Another solution: how to rotate a matrix faster {#another-solution-how-to-rotate-a-matrix-faster}

Swap the diagnoal elements and reverse each line in the matrix.

| 1 | 2 | 3 | swap | 1 | 4 | 7 | reverse | 7 | 4 | 1 |
|---|---|---|------|---|---|---|---------|---|---|---|
| 4 | 5 | 6 | ---> | 2 | 5 | 8 | ------> | 8 | 5 | 2 |
| 7 | 8 | 9 |      | 3 | 6 | 9 |         | 9 | 6 | 3 |


## Solution {#solution}


### Solution 1: Straightforward {#solution-1-straightforward}

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n//2):
            # Shrink the dimension
            # Do not include the last element
            for j in range(i, n-i-1):
                tmp = matrix[i][j]
                matrix[i][j] = matrix[n-1-j][i]
                matrix[n-1-j][i] = matrix[n-1-i][n-1-j]
                matrix[n-1-i][n-1-j] = matrix[j][n-1-i]
                matrix[j][n-1-i] = tmp

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
Solution().rotate(matrix)
[print(*line) for line in matrix]
```


### Solution 2: {#solution-2}

```python
class Solution(object):
    def rotate(self, matrix):
        """
        :type matrix: List[List[int]]
        :rtype: None Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        for i in range(n):
            matrix[i].reverse()

matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
Solution().rotate(matrix)
[print(*line) for line in matrix]
```

[48. Rotate Image](https://leetcode.com/problems/rotate-image/)
