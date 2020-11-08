+++
title = "128 - Longest Consecutive Sequence"
lastmod = 2020-05-02T16:34:20+02:00
tags = ["hard", "array", "1-pass", "1-hint"]
categories = ["leetcode"]
draft = true
+++

[leetcode](https://leetcode.com/problems/longest-consecutive-sequence/)


## Problem {#problem}

```text
Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

Your algorithm should run in O(n) complexity.

Example:

Input: [100, 4, 200, 1, 3, 2]
Output: 4
Explanation: The longest consecutive elements sequence is [1, 2, 3, 4]. Therefore its length is 4.
```


## Solution {#solution}


### Solution 1: Hash Map {#solution-1-hash-map}

For each value, we maintain the left bound and right bound of range and also update the bounds for left value and right value.

```python
class Solution:
    def longestConsecutive(self, nums):
        h = dict()
        ans = 0

        for num in nums:
            if num not in h:
                if num - 1 in h and num + 1 in h:
                    h[h[num + 1][1]][0] = h[num - 1][0]
                    h[h[num - 1][0]][1] = h[num + 1][1]
                    h[num] = [h[num - 1][0], h[num + 1][1]]
                elif num - 1 in h:
                    h[h[num - 1][0]][1] += 1
                    h[num] = h[h[num - 1][0]]
                elif num + 1 in h:
                    h[h[num + 1][1]][0] -= 1
                    h[num] = h[h[num + 1][1]]
                else:
                    h[num] = [num, num]
                ans = max(ans, h[num][1] - h[num][0] + 1)

        return ans
```

Time: O(n)

Space: O(n)


### Solution 2: Keep Counting! {#solution-2-keep-counting}

Notice the `if x - t not in nums`.

```python
class Solution:
    def longestConsecutive(self, nums):
        ans = 0
        nums = set(nums)
        for x in nums:
            if x - 1 not in nums:
                y = x + 1
                while y in nums:
                    y += 1
                ans = max(ans, y - x)
        return ans
```

Time: O(n)

Space: O(n)
