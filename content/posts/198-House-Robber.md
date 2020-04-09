+++
title = "198 - House Robber"
date = 2020-03-27T23:58:00+01:00
lastmod = 2020-03-29T17:42:39+02:00
tags = ["easy", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/house-robber/)


## Problem {#problem}

```text
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:

Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.
Example 2:

Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.
```


## Notes {#notes}

States: 1. house, 2. rob or not rob -> dp[i][0 or 1]

Transition: dp[i][0] = max(dp[i-1][0], dp[i-1][1]), dp[i][1] = dp[i-1][0] + nums[i]

Base Case: dp[0][0] = 0, dp[0][1] = 0


## Solution {#solution}

```python
class Solution:
    def rob(self, nums):
        robbed, notRobbed = 0, 0
        for i in nums:
            robbed, notRobbed = notRobbed + i, max(robbed, notRobbed)
        return max(robbed, notRobbed)
```
