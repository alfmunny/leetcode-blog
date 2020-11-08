+++
title = "448 - Find All Numbers Disappeard in an Array"
date = 2020-04-28T17:10:00+02:00
lastmod = 2020-04-30T10:08:27+02:00
tags = ["easy", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/)


## Problem {#problem}

Given an array of integers where 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements of [1, n] inclusive that do not appear in this array.

Could you do it without extra space and in O(n) runtime? You may assume the returned list does not count as extra space.

Example:

Input:
[4,3,2,7,8,2,3,1]

Output:
[5,6]


## Solution {#solution}

Move all the numbers to its position. For example, 4 move to index 3, 3 move to index 2 and so on.

The numbers at index i, which are not equal i + 1, are the ones disappeared.

The operation is in-place.

```python
class Solution:
    def findDisappearedNumbers(self, nums):
        for i in nums:
            j = i
            while nums[j-1] != j:
                nums[j-1], j = j, nums[j-1]

        return [i+1 for i in range(len(nums)) if nums[i] != i+1]
```

Time: O(N)

Space: O(1)
