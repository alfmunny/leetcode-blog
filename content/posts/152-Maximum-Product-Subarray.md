+++
title = "152 - Maximum Product Subarray"
date = 2020-03-29T17:40:00+02:00
lastmod = 2020-03-29T17:42:51+02:00
tags = ["medium", "array", "dp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/maximum-product-subarray/)


## Problem {#problem}

```text
Given an integer array nums, find the contiguous subarray within an array (containing at least one number) which has the largest product.

Example 1:

Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
Example 2:

Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```


## Notes {#notes}

DP problem:

-   States:
    We have to know two previous states to deduct the current max product:

    -   index
    -   max for positive or min for negative

    So the DP Table is dp[i(index)][0 or 1(max or min)]

-   Transition:
    -   if nums[i] >= 0:
        dp[i][0] = max(nums[i], dp[i-1][0] \* nums[i])
        dp[i][1] = dp[i-1][1] \* nums[i]

    -   if nums[i] < 0:

        dp[i][0] = dp[i-1][1] \* nums[i])
        dp[i][1] = min(nums[i], dp[i-1][0] \* nums[i]

-   Base case:

    if there is only one element:

    dp[0][0] = dp[0][1] = nums[0]


## Solution {#solution}


### Solution 1: DP {#solution-1-dp}

Original Version:

```python
class Solution:
    def maxProduct(self, nums):
        if not nums:
            return 0

        dp = [[0] * 2 for i in range(len(nums))]
        res = dp[0][0] = dp[0][1] = nums[0]

        for i in range(1, len(nums)):
            if nums[i] >= 0:
                dp[i][0] = max(nums[i], dp[i - 1][0] * nums[i])
                dp[i][1] = dp[i - 1][1] * nums[i]
            else:
                dp[i][0] = dp[i - 1][1] * nums[i]
                dp[i][1] = min(nums[i], nums[i] * dp[i - 1][0])
            res = max(res, dp[i][0])
        return res
```

Simplify Version 1:

```python
class Solution:
    def maxProduct(self, nums):
        if not nums:
            return 0

        pos = neg = res = nums[0]
        for i in nums[1:]:
            if i>=0:
                pos = max(i, pos*i)
                neg = neg*i
            else:
                tmp = pos # Important: remember the value, because we are gonna alter it.
                pos = neg*i
                neg = min(tmp*i, i) # Use the original value
                # We also can write as this, but we should notice it only works in like python or ruby
                # pos, neg = neg*i, min(pos*i, i), simplify to version 3
            res = max(pos, res)
        return res
```

Simplify Version 2:

```python
class Solution:
    def maxProduct(self, nums):
        if not nums:
            return 0

        pos = neg = res = nums[0]
        for i in nums[1:]:
            if i>=0:
                pos, neg = max(i, pos*i), neg*i
            else:
                pos, neg = neg*i, min(i, pos*i)
            res = max(pos, res)
        return res
```


### Solution 2: Prefix sum and Suffix sum {#solution-2-prefix-sum-and-suffix-sum}

```python
class Solution:
    def maxProduct(self, nums):
        rnums = nums[::-1]
        for i in range(1, len(nums)):
            nums[i] *= nums[i-1] or 1
            rnums[i] *= rnums[i-1] or 1
        return max(nums, rnums)
```
