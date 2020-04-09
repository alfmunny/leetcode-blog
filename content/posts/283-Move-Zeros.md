+++
title = "283 - Move Zeros"
date = 2020-04-04T17:20:00+02:00
lastmod = 2020-04-04T17:21:44+02:00
tags = ["easy", "array", "two-pointer", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/move-zeroes/)


## Problem {#problem}

```text
Given an array nums, write a function to move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Example:

Input: [0,1,0,3,12]
Output: [1,3,12,0,0]
Note:

You must do this in-place without making a copy of the array.
Minimize the total number of operations.
```


## Solution {#solution}

Two pointers.

One pointer is for the start of 0.

One pointer keeps going forward.

```python
class Solution:
    def moveZeros(self, nums):

        p1, p2 = 0, 0

        for p2 < len(nums):
            if nums[p1] != 0:
                p1 += 1
            elif nums[p2] != 0:
                nums[p1], nums[p2] = nums[p2], nums[p1]
                p1 += 1
            p2 += 1

        return nums
```
