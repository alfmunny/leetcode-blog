+++
title = "556 - Next Greater Element III"
date = 2020-11-26T01:18:00+01:00
lastmod = 2020-11-26T01:19:55+01:00
tags = ["medium", "array", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/next-greater-element-iii/)


## Problem {#problem}

```text
Given a positive 32-bit integer n, you need to find the smallest 32-bit integer which has exactly the same digits existing in the integer n and is greater in value than n. If no such positive 32-bit integer exists, you need to return -1.

Example 1:

Input: 12
Output: 21


Example 2:

Input: 21
Output: -1
```


## Solution {#solution}

```python
class Solution:
    def nextGreaterElement(self, n: int) -> int:
        s = list(str(n))

        first = len(s) - 1
        for i in range(len(s)-2, -1, -1):
            if s[i] < s[i+1]:
                first = i
                break

        if first == len(s) - 1:
            return -1

        second = first+1
        minimum = s[second]

        for i in range(first+1, len(s)):
            if s[i] < minimum and s[i] > s[first]:
                minumum = s[i]
                second = i

        s[first], s[second] = s[second], s[first]

        ret = int("".join(s[:first+1] + sorted(s[first+1:])))
        return ret if ret <= (1<<31-1) else -1
```
