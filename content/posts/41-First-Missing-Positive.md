+++
title = "41 - First Missing Positive"
author = ["alfmunny"]
lastmod = 2020-03-14T10:18:55+01:00
tags = ["hard", "array", "constant-memory"]
categories = ["leetcode"]
draft = false
+++

## Problem {#problem}

```text
Given an unsorted integer array, find the smallest missing positive integer.

Example 1:

Input: [1,2,0]
Output: 3

Example 2:

Input: [3,4,-1,1]
Output: 2

Example 3:

Input: [7,8,9,11,12]
Output: 1

Note:

Your algorithm should run in O(n) time and uses constant extra space.
```


## Notes {#notes}

Run in O(n) time and uses constant extra space

1.  Say the length of the array is l, the number must be in 1...l+1 (also l possible numbers)

    For example

    [1, 2, 3, 4], the first missing positive is 5.

    [7, 8, 9, 10], the first missing positive is 1

    It means you can use the array as a constant space. The result must be (one of the indexes + 1).

2.  We put the number in the right place. When it is 10, we swap it with A[9].

After all the numbers are in the right place, the first one, whose index + 1 != number, it is the missing one


### How to put the numer in the right place {#how-to-put-the-numer-in-the-right-place}

Use the \`while\` to swap the numbers. Only \`if\` can not do the same job.

Consider nums = [3, 4, -1, 1].

Only with if:

First Loop: swap 3 and -1

nums = [-1, 4, 3, 1]

Second Loop: swap 4 and 1

nums = [-1, 1, 3, 4]

And the process stops. Because 4 is already in the right place. You miss to put the 1 in the right place.

So you have to do it recursively, with \`while\`.


## Solution {#solution}

```python
class Solution(object):
    def firstMissingPositive(self, nums):
        l = len(nums)
        for i in range(l):
            # Note!: here has to be using while
            while (nums[i] > 0 and nums[i] <= l and nums[nums[i] - 1] != nums[i]):
                nums[nums[i]-1], nums[i] = nums[i], nums[nums[i]-1]

        for i, n in enumerate(nums):
            if (n != i+1):
                return i + 1

        return l + 1

print(Solution().firstMissingPositive([1, -1, 3, 4]))
```
