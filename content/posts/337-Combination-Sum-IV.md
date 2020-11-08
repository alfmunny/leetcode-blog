+++
title = "377 - Combination Sum IV"
date = 2020-06-11T15:12:00+02:00
lastmod = 2020-06-11T15:13:10+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/combination-sum-iv/submissions/)


## Problem {#problem}

```text
Given an integer array with all positive numbers and no duplicates, find the number of possible combinations that add up to a positive integer target.

Example:

nums = [1, 2, 3]
target = 4

The possible combination ways are:
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

Note that different sequences are counted as different combinations.

Therefore the output is 7.
```


## Solution {#solution}

```python
class Solution:
    def combinationSum4(self, nums, target):
        dp = [0] * (target + 1)
        dp[0] = 1

        for i in range(target+1):
            for j in nums:
                if i < j:
                    continue
                dp[i] += dp[i-j]

        return dp[-1]
```
