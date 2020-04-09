+++
title = "215 - Kth Largest Element in an Array"
date = 2020-04-06T01:05:00+02:00
lastmod = 2020-04-08T11:26:32+02:00
tags = ["medium", "array", "divide", "recursive", "1-pass", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/kth-largest-element-in-an-array/)


## Problem {#problem}

```text
215. Kth Largest Element in an Array
Medium

3152

222

Add to List

Share
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Example 1:

Input: [3,2,1,5,6,4] and k = 2
Output: 5
Example 2:

Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4
Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
```


## Solution {#solution}

The naive solution would be to maintain an array of length k and update the array
in each iteration to keep the first kth largest element in the array


### Solution 1: Array of k {#solution-1-array-of-k}

```python
class Solution:
    def findKthLargest(self, nums, k):
        l = []

        for i in nums:
            if not l:
                l.append(i)
            else:
                len0 = len(l)
                for j in range(len(l)):
                    if i >= l[j]:
                        l = l[0:j] + [i] + l[j:]
                        break
                if len0 == len(l) and len0 != k:
                    l.append(i)
                l = l[0:k]
        return l[-1]
```

Time: O(nk)

Space: O(k)


### Solution 2: Partition to find the kth largest {#solution-2-partition-to-find-the-kth-largest}

```python
class Solution:
    def findKthLargest(self, nums, k):
        pos = self.partition(nums, 0, len(nums) - 1)
        if pos + 1 < k:
            return self.findKthLargest(nums[pos + 1:], k - pos - 1)
        elif pos + 1 > k:
            return self.findKthLargest(nums[0:pos], k)
        else:
            return nums[pos]

    def partition(self, nums, l, r):
        p = r

        while(l < r):
            while l < r and nums[l] > nums[p]:
                l += 1
            while l < r and nums[r] <= nums[p]:
                r -= 1
            nums[l], nums[r] = nums[r], nums[l]
        nums[l], nums[p] = nums[p], nums[l]
        return l
```

Time: O(klogn)

Space: O(1)
