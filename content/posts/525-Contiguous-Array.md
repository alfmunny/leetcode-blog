+++
title = "525 - Contiguous Array"
date = 2020-04-13T23:06:00+02:00
lastmod = 2020-04-13T23:22:40+02:00
tags = ["medium", "array", "hash", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/contiguous-array)


## Problem {#problem}

```text
Given a binary array, find the maximum length of a contiguous subarray with equal number of 0 and 1.

Example 1:
Input: [0,1]
Output: 2
Explanation: [0, 1] is the longest contiguous subarray with equal number of 0 and 1.
Example 2:
Input: [0,1,0]
Output: 2
Explanation: [0, 1] (or [1, 0]) is a longest contiguous subarray with equal number of 0 and 1.
Note: The length of the given binary array will not exceed 50,000.
```


## Solution {#solution}

We keep a count, which decrease 1 if 0, increase 1 if 1.

If at x and y, they have the same value v of count, then the numbers between x+1 and y have the equal number of 1s and 0s. The max length = y - (x + 1) + 1 = y - x

And after that, if we found at index w, it also has value v of count. The max length should be w - x.

So we have to maintain a hashmap h using the values of count as keys, and the first index of that count as its value.

The `maxlen = max(maxlen, h[count])` if current count in the map.

**Important**

We have an initial value of the map.

h[0] = -1 (If count == 0 at index i, we have all the numbers between h[0] + 1 and i. And h[0] + 1 should at index 0, so h[0] = -1)

Consider the input [0, 1]:

```text
Index 0: h[-1] = 0, maxlen = 0
Index 1: h[0] = -1, maxlen = 1 - (-1) = 2
maxlen = 2
```

```python
class Solution:
    def findMaxLength(self, nums):
        h = {0: -1}

        count = ans = 0
        for i in range(len(nums)):
            count += 1 if nums[0] else -1
            ans = max(ans, h.setdefault(count, i))

        return ans
```
