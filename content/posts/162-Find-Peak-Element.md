+++
title = "162 - Find Peak Element"
date = 2020-06-18T16:09:00+02:00
lastmod = 2020-06-18T16:12:10+02:00
tags = ["medium", "array", "bs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/find-peak-element/)


## Problem {#problem}

```text
A peak element is an element that is greater than its neighbors.

Given an input array nums, where nums[i] ≠ nums[i+1], find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that nums[-1] = nums[n] = -∞.

Example 1:

Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
Example 2:

Input: nums = [1,2,1,3,5,6,4]
Output: 1 or 5
Explanation: Your function can return either index number 1 where the peak element is 2,
             or index number 5 where the peak element is 6.
```


## Solution {#solution}

```python
class Solution:
    def findPeakElement(self, nums: List[int]) -> int:
        if len(nums) == 1:
            return 0
        if len(nums) == 2:
            return 0 if nums[0] > nums[1] else 1

        l = 1
        r = len(nums) - 2

        while l <= r:
            mid = (r + l) // 2
            if nums[mid-1] < nums[mid] > nums[mid+1]:
                return mid
            elif nums[mid] <= nums[mid+1]:
                l = mid + 1
            else:
                r = mid - 1

        if nums[0] > nums[1]:
            return 0
        elif nums[-1] > nums[-2]:
            return len(nums) - 1
```
