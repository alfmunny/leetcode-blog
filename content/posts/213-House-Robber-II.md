+++
title = "213 - House Robber II"
date = 2020-06-08T23:24:00+02:00
lastmod = 2020-06-08T23:24:29+02:00
tags = ["medium", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/house-robber-ii/)


## Problem {#problem}

```text
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are arranged in a circle. That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:

Input: [2,3,2]
Output: 3
Explanation: You cannot rob house 1 (money = 2) and then rob house 3 (money = 2),
             because they are adjacent houses.
Example 2:

Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
```


## Solution {#solution}

Two loops of dp:

1.  consider the array from 0 to n - 2
2.  consider the array from 1 to n - 1
3.  return the max value from this two loops

<!--listend-->

```python
class Solution:
    def rob(self, nums):
        if not nums:
            return 0
        if len(nums) == 1:
            return nums[0]

        rob = nrob = rob2 = nrob2 = 0

        for n in range(1, len(nums)):
            rob, nrob = nrob + nums[n], max(rob, nrob)
            rob2, nrob2 = nrob2 + nums[n - 1], max(rob2, nrob2)

        return max(rob, nrob, rob2, nrob2)
```
