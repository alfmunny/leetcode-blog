+++
title = "81 - Search in Rotated Sorted Array II"
date = 2020-08-13T23:48:00+02:00
lastmod = 2020-08-13T23:52:23+02:00
tags = ["medium", "array", "bs", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/search-in-rotated-sorted-array-ii/)


## Problem {#problem}

```text
Suppose an array sorted in ascending order is rotated at some pivot unknown to you beforehand.

(i.e., [0,0,1,2,2,5,6] might become [2,5,6,0,0,1,2]).

You are given a target value to search. If found in the array return true, otherwise return false.

Example 1:

Input: nums = [2,5,6,0,0,1,2], target = 0
Output: true
Example 2:

Input: nums = [2,5,6,0,0,1,2], target = 3
Output: false
Follow up:

This is a follow up problem to Search in Rotated Sorted Array, where nums may contain duplicates.
Would this affect the run-time complexity? How and why?
```


## Solution {#solution}

Note:

Consider the problem in two part:

1.  when the left part is in order
2.  when the right part is in order

Important: How to guarentee the left part is in order when there is duplicates in the array:
We can use a `while` to eliminate the duplicates if nums[left] == nums[mid]

```python
class Solution:
    def search(self, nums: List[int], target: int) -> bool:
        if not nums:
            return False

        left = 0
        right = len(nums) - 1

        while left < right:
            mid = (left + right) // 2

            if nums[mid] == target:
                return True

            while left < mid and nums[left] == nums[mid]:
                left += 1

            if nums[mid] >= nums[left]:
                if nums[mid] > target >= nums[left]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
            print(left, right)

        return target == nums[left]
```
