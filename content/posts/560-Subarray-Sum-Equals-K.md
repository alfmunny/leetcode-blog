+++
title = "560 Subarray Sum Equals K"
date = 2020-04-23T01:38:00+02:00
lastmod = 2020-04-23T01:39:41+02:00
tags = ["medium", "array", "hash", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/subarray-sum-equals-k/)


## Problem {#problem}

```text
Given an array of integers and an integer k, you need to find the total number of continuous subarrays whose sum equals to k.

Example 1:
Input:nums = [1,1,1], k = 2
Output: 2
Note:
The length of the array is in range [1, 20,000].
The range of numbers in the array is [-1000, 1000] and the range of the integer k is [-1e7, 1e7].
```


## Solution {#solution}

```python
class Solution:
    def subArraySum(self, nums, k):
        h = {0: 1}
        s = 0
        ans = 0
        for i in nums:
            s += i
            ans += h.get(s-k, 0)
            h[s] = h.get(s, 0) + 1

        return ans
```
