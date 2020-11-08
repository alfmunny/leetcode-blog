+++
title = "540 - Single Element in a Sorted Array"
date = 2020-05-12T18:43:00+02:00
lastmod = 2020-05-14T22:14:21+02:00
tags = ["medium", "array", "bs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/single-element-in-a-sorted-array/)


## Problem {#problem}

> You are given a sorted array consisting of only integers where every element appears exactly twice,
> except for one element which appears exactly once. Find this single element that appears only once.
>
> Example 1:
>
> Input: [1,1,2,3,3,4,4,8,8]
> Output: 2
>
> Example 2:
>
> Input: [3,3,7,7,10,11,11]
> Output: 10


## Solution {#solution}

```python
class Solution:
    def singleNonDuplicate(self, nums):
        lo = 0
        hi = len(nums) - 1

        while lo < hi:
            mid = (lo + hi) // 2
            if mid == 0:
                return mid

            if (mid - lo + 1) % 2 == 0:
                if nums[mid] == nums[mid - 1]:
                    lo = mid + 1
                else:
                    hi = mid - 1
            else:
                if nums[mid] == nums[mid - 1]:
                    hi = mid - 2
                else:
                    lo = mid
        return nums[lo]

print(Solution().singleNonDuplicate([1,1,2,3,3,5,5,10,10]))
```
