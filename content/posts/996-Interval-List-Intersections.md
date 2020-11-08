+++
title = "986 - Interval List Intersections"
date = 2020-05-24T01:13:00+02:00
lastmod = 2020-05-24T01:14:14+02:00
tags = ["medium", "array", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/interval-list-intersections/)


## Problem {#problem}

```text
Given two lists of closed intervals, each list of intervals is pairwise disjoint and in sorted order.

Return the intersection of these two interval lists.

(Formally, a closed interval [a, b] (with a <= b) denotes the set of real numbers x with a <= x <= b.  The intersection of two closed intervals is a set of real numbers that is either empty, or can be represented as a closed interval.  For example, the intersection of [1, 3] and [2, 4] is [2, 3].)

Example 1:

Input: A = [[0,2],[5,10],[13,23],[24,25]], B = [[1,5],[8,12],[15,24],[25,26]]
Output: [[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
Reminder: The inputs and the desired output are lists of Interval objects, and not arrays or lists.
```


## Solution {#solution}

```python
class Solution:
    def intervalListIntersection(self, A, B):
        ans = []
        i = j = 0

        while i < len(A) and j < len(B):
            left = max(A[i][0], B[j][0])
            right = min(A[i][1], B[j][1])
            if left <= right:
                ans.append([left, right])
            if A[i][1] < B[j][1]:
                i += 1
            else:
                j += 1

        return ans
```
