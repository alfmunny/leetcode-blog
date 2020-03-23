+++
title = "53 - Maximum Subarray"
author = ["alfmunny"]
lastmod = 2020-03-21T22:16:34+01:00
tags = ["easy", "array", "dp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/maximum-subarray/)


## Problem {#problem}

```text
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:

Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:

If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
```


## Notes {#notes}

Dynamic programming problem.

Use nums[i] always store the maximum sum.

maxSum(i) = maxSum(i-1) + nums[i] only if maxSum(i-1) > 0


## Solution {#solution}


### Solution 1: use a extra dp array {#solution-1-use-a-extra-dp-array}

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        curSum = maxSum = nums[0]

        for num in nums[1:]:
          curSum = max(num, curSum+num)
          maxSum = max(curSum, maxSum)

        return maxSum

print(Solution().maxSubArray([-2,1,-3,4,-1,2,1,-5,4]))
```


### Solution 2: no extra space, in place modify {#solution-2-no-extra-space-in-place-modify}

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """

        if len(nums) == 0:
            return 0

        ret = nums[0]

        for i in range(1, len(nums)):
            if nums[i - 1] > 0:
                nums[i] += nums[i - 1]

            ret = max(ret, nums[i])

        return ret
print(Solution().maxSubArray([-2,1,-3,4,-1,2,1,-5,4]))
```
