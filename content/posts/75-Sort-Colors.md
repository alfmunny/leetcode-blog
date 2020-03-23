+++
title = "75 - Sort Colors"
author = ["alfmunny"]
date = 2020-03-06T17:26:00+01:00
lastmod = 2020-03-21T22:31:33+01:00
tags = ["medium", "array", "sort"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/sort-colors/)


## Problem {#problem}

```text
Given an array with n objects colored red, white or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white and blue.

Here, we will use the integers 0, 1, and 2 to represent the color red, white, and blue respectively.

Note: You are not suppose to use the library's sort function for this problem.

Example:

Input: [2,0,2,1,1,0]
Output: [0,0,1,1,2,2]
Follow up:

A rather straight forward solution is a two-pass algorithm using counting sort.
First, iterate the array counting number of 0's, 1's, and 2's, then overwrite array with total number of 0's, then 1's and followed by 2's.
Could you come up with a one-pass algorithm using only constant space?
```


## Notes {#notes}


### First attempt is to use two pointer. {#first-attempt-is-to-use-two-pointer-dot}

There is a but a corner case: when two pointer are both at 1. How should we move the pointer.

We can use a another `while` unter this situation, initialize another pointer and search for 0 or 2 between
these two pointers. See Soution 1


### Three Way Partition {#three-way-partition}

three pointer, one for each.

**Important**:

Notice the condition for `while`: while mi <= hi

the middle move forward:

1.  middle == 0, switch with left one, left + 1, middle + 1
2.  middle == 1, continue
3.  middle == 2, swtich with right one, right - 1


## Solution {#solution}


### Solution 1 {#solution-1}

```python
class Solution(object):
    def sortColors(self, nums):
        """
        :type nums: List[int]
        :rtype: None Do not return anything, modify nums in-place instead.
        """

        lo = 0
        hi = len(nums) - 1

        while (lo < hi):
            if nums[lo] == 0:
                lo += 1
            elif nums[hi] == 2:
                hi -= 1
            elif nums[lo] == 1 and nums[hi] == 1:
                mi = lo + 1
                while (mi < hi):
                    if nums[mi] == 2 or nums[mi] == 0:
                        nums[mi], nums[hi] = nums[hi], nums[mi]
                        break
                    else:
                        mi += 1
                if mi == hi:
                    return
            else:
                nums[lo], nums[hi] = nums[hi], nums[lo]
```


### Solution 2: Three way partition {#solution-2-three-way-partition}

Notice the condition for `while`:

It has to be <=.
Because you every element behind hi, you have seen it.
But not the element at hi. You have to check it at last.

```python
class Solution(object):
    def sortColors(self, nums):

        lo, mi, hi = 0, 0, len(nums) - 1

        while mi <= hi: # Nottice!: here has to be <=
            if nums[mi] == 0:
                nums[mi], nums[lo] = nums[lo], nums[mi]
                lo += 1
                mi += 1
            elif nums[mi] == 2:
                nums[mi], nums[hi] = nums[hi], nums[mi]
                hi -= 1
            else:
                mi += 1
```
