+++
title = "303 - Range Sum Query - Immutable"
date = 2020-06-27T15:52:00+02:00
lastmod = 2020-06-27T15:54:19+02:00
tags = ["easy", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/range-sum-query-immutable/)


## Problem {#problem}

```text
Given an integer array nums, find the sum of the elements between indices i and j (i ≤ j), inclusive.

Example:
Given nums = [-2, 0, 3, -5, 2, -1]

sumRange(0, 2) -> 1
sumRange(2, 5) -> -1
sumRange(0, 5) -> -3
Note:
You may assume that the array does not change.
There are many calls to sumRange function.
```


## Solution {#solution}

```python
class NumArray:
    def __init__(self, nums: List[int]):
        self.dp = list(nums)
        self.dp.insert(0, 0)
        for i in range(1, len(nums)):
            self.dp[i+1] += self.dp[i]

    def sumRange(self, i: int, j: int) -> int:
        return self.dp[j+1] - self.dp[i]
```
