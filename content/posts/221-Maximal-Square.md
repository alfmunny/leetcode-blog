+++
title = "221 - Maximal Square"
date = 2020-03-30T20:21:00+02:00
lastmod = 2020-03-30T21:46:17+02:00
tags = ["medium", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/maximal-square/)


## Problem {#problem}

```text
Given a 2D binary matrix filled with 0's and 1's, find the largest square containing only 1's and return its area.

Example:

Input:

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

Output: 4
```


## Notes {#notes}

DP Problem:

-   States:

    -   position -> [i][j]
    -   how many continues 1 in vertical direction -> [i][j][0]
    -   how many continues 1 in horizontal direction -> [i][j][1]
    -   square value(or the length of the square) -> [i][j][2]

    dp[i][j][0 or 1 or 2]

-   Transition:

    ```text
    dp[i + 1][j + 1][0] = dp[i][j + 1][0] + 1
    dp[i + 1][j + 1][1] = dp[i + 1][j][1] + 1
    dp[i + 1][j + 1][2] = min(dp[i][j][2]+1, dp[i + 1][j + 1][0], dp[i + 1][j + 1][1])
    ```

<!--listend-->

-   Base Case:

    One padding row on vertical and horizontal direction, with value 0


## Solution {#solution}

Original Version
:

<!--listend-->

```python
class Solution:
    def maximalSquare(self, matrix):
        if not matrix:
            return 0

        dp = [[[0] * 3 for j in range(len(matrix[0]) + 1)] for i in range(len(matrix) + 1)]
        res = 0
        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == "1":
                    dp[i + 1][j + 1][0] = dp[i][j + 1][0] + 1
                    dp[i + 1][j + 1][1] = dp[i + 1][j][1] + 1
                    dp[i + 1][j + 1][2] = min(dp[i][j][2]+1, dp[i + 1][j + 1][0], dp[i + 1][j + 1][1])
                    res = max(res, dp[i + 1][j + 1][2])

        return res*res
```

Time: O(mn)
Space: O(mn)

Simplified Version 1: optimize the space, 3xn space
:

<!--listend-->

```python
class Solution:
    def maximalSquare(self, matrix):
        if not matrix:
            return 0

        dp = [[0] * 3 for j in range(len(matrix[0]) + 1)]
        res = 0

        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                if matrix[i][j] == "1":
                    dp[j+1][0] = dp[j+1][0] + 1
                    dp[j+1][1] = dp[j][1] + 1
                    dp[j+1][2] = min(dp[j+1][2]+1, dp[j+1][0]+1, dp[j][1]+1)
                    res = max(res, dp[j + 1][2])
                else:
                    dp[j+1][0] = dp[j+1][1] = dp[j+1][2] = 0

        return res*res
```

Space: O(n)

Simplified Version 2: n space
:

<!--listend-->

```python
class Solution:
    def maximalSquare(self, matrix):
        if not matrix:
            return 0

        dp = [0 for j in range(len(matrix[0]) + 1)]
        res = 0
        prev = 0 # previous diagnol element

        for i in range(len(matrix)):
            for j in range(len(matrix[0])):
                temp = dp[j+1]
                if matrix[i][j] == "1":
                    dp[j+1] = min(prev, dp[j+1], dp[j]) + 1
                    res = max(res, dp[j + 1])
                else:
                    dp[j+1] = 0

                prev = temp

        return res*res
```

Simplified Version 3: in place
:

<!--listend-->

```python
class Solution:
    def maximalSquare(self, matrix):
        if not matrix:
            return 0
        res = 0
        m = len(matrix)
        n = len(matrix[0])

        for i in range(m):
            for j in range(n):
                if matrix[i][j] == "1":
                    if i == 0 or j == 0:
                        matrix[i][j] = 1
                    else:
                        matrix[i][j] = min(matrix[i - 1][j - 1],
                                           matrix[i][j - 1],
                                           matrix[i - 1][j]) + 1
                    res = max(res, matrix[i][j])
                else:
                    matrix[i][j] = 0

        return res * res
```

Space: O(1)
