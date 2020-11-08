+++
title = "Leftmost Column with at Least a One"
date = 2020-04-22T01:20:00+02:00
lastmod = 2020-04-23T01:21:53+02:00
tags = ["medium", "array", "1-pass", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/explore/featured/card/30-day-leetcoding-challenge/530/week-3/3306)


## Problem {#problem}

```text
A binary matrix means that all elements are 0 or 1. For each individual row of the matrix, this row is sorted in non-decreasing order.

Given a row-sorted binary matrix binaryMatrix, return leftmost column index(0-indexed) with at least a 1 in it. If such index doesn't exist, return -1.

You can't access the Binary Matrix directly.  You may only access the matrix using a BinaryMatrix interface:

BinaryMatrix.get(x, y) returns the element of the matrix at index (x, y) (0-indexed).
BinaryMatrix.dimensions() returns a list of 2 elements [m, n], which means the matrix is m * n.
Submissions making more than 1000 calls to BinaryMatrix.get will be judged Wrong Answer.  Also, any solutions that attempt to circumvent the judge will result in disqualification.

For custom testing purposes you're given the binary matrix mat as input in the following four examples. You will not have access the binary matrix directly.

Example 1:

Input: mat = [[0,0],[1,1]]
Output: 0

Example 4:
Input: mat = [[0,0,0,1],[0,0,1,1],[0,1,1,1]]
Output: 1
```


## Solution {#solution}

```python
# """
# This is BinaryMatrix's API interface.
# You should not implement it, or speculate about its implementation
# """
#class BinaryMatrix(object):
#    def get(self, x: int, y: int) -> int:
#    def dimensions(self) -> list[]:
class Solution:
    def leftMostColumnWithOne(self, binaryMatrix):
        n, m = binaryMatrix.dimensions()
        ans = m
        for i in range(n):
            x = self.findOne(binaryMatrix, i, 0, m - 1)
            if x != -1:
                ans = min(ans, x)
        return ans if ans != m else -1

    def findOne(self, m, r, i, j):
        if i == j:
            return i if m.get(r, i) == 1 else -1

        mid = (i + j) // 2
        if m.get(r, mid) == 1:
            if mid == 0 or m.get(r, mid - 1) == 0:
                return mid
            else:
                return self.findOne(m, r, i, mid - 1)
        else:
            return self.findOne(m, r, mid+1, j)
```
