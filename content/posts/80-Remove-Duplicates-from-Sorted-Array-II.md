+++
title = "80 - Remove Duplicates from Sorted Array II"
date = 2020-08-13T22:21:00+02:00
lastmod = 2020-08-13T22:35:26+02:00
tags = ["medium", "array", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)


## Problem {#problem}

```text
Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:

Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.
```


## Solution {#solution}

Keep a pointer to copy the value from behind.

Very interesting solution: n > nums[i-k], where k = 2

```python
class Solution:
    def removeDuplicates(self, nums):
        i = 0
        k = 2
        for n in nums:
            if i < k or n > nums[i-k]:
                nums[i] = n
                i += 1
        return i
```
