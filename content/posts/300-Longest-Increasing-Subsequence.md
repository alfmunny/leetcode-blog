+++
title = "300 - Longest Increasing Subsequence"
date = 2020-03-28T00:08:00+01:00
lastmod = 2020-03-28T00:14:41+01:00
tags = ["medium", "dp", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/longest-increasing-subsequence/)


## Problem {#problem}

```text
Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:

Input: [10,9,2,5,3,7,101,18]
Output: 4
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
Note:

There may be more than one LIS combination, it is only necessary for you to return the length.
Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?
```


## Notes {#notes}


### Solution 1: DP with O(n^2) {#solution-1-dp-with-o--n-2}

DP problem

States: index, dp[index] = longest increasing subsequence at this position

Transition: if nums[j] < nums[i]: dp[i] = max(dp[i], dp[j] + 1)

Base Case: dp[0] = 1


### Solution 2: DP with binary search {#solution-2-dp-with-binary-search}


## Solution {#solution}


### Solution 1: DP with O(n^2) {#solution-1-dp-with-o--n-2}

```python
class Solution:
    def lengthOfLIS(self, nums):
        dp = [1] * len(nums)

        for i in range(1, len(nums)):
            for j in range(i):
                if nums[j] < nums[i]:
                    dp[i] = max(dp[i], dp[j] + 1)

        return max(dp) if nums else 0
```


### <span class="org-todo todo TODO">TODO</span> Solution 2: DP with binary search {#solution-2-dp-with-binary-search}
