+++
title = "169 - Majority Element"
date = 2020-04-28T16:22:00+02:00
lastmod = 2020-04-28T16:31:52+02:00
tags = ["easy", "array", "hash", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/majority-element/)


## Problem {#problem}

Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:

Input: [3,2,3]
Output: 3

Example 2:

Input: [2,2,1,1,1,2,2]
Output: 2


## Solution {#solution}


### Solution 1: Hash Table {#solution-1-hash-table}

```python
from collections import Counter
class Solution:
    def majorityElement(self, nums):
        c = Counter()
        l = len(nums)
        for n in nums:
            c[n] += 1
            if c[n] > l/2:
                return n

print(Solution().majorityElement([1, 1, 2, 2, 2, 2, 4]))
```

Time: O(n)

Space: O(n)


### Solution 2: Boyer-Moore Majority Vote Algorithm {#solution-2-boyer-moore-majority-vote-algorithm}

<http://www.cs.utexas.edu/~moore/best-ideas/mjrty/index.html>

This algorithm works only when the majorty exists.

For array like [1, 1, 2, 2, 2, 1], it return 2. But it is not a majority element.

```python
class Solution:
    def majorityElement(self, nums):
        counter = 1
        ans = nums[0]

        for n in nums[1:]:
            if n == ans:
                counter += 1
            else:
                counter -= 1
                if counter < 0:
                    counter = 1
                    ans = n
        return ans
print(Solution().majorityElement([1, 1, 2, 2, 2, 2, 4]))
```

Time: O(n)

Space: O(1)
