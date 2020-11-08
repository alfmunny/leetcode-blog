+++
title = "264 - Ugly Number II"
date = 2020-06-27T23:37:00+02:00
lastmod = 2020-06-27T23:37:44+02:00
tags = ["medium", "array", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/ugly-number-ii/)


## Problem {#problem}

```text
Write a program to find the n-th ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.

Example:

Input: n = 10
Output: 12
Explanation: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 is the sequence of the first 10 ugly numbers.
Note:

1 is typically treated as an ugly number.
n does not exceed 1690.
```


## Solution {#solution}

```python
class Solution:
    ugly = sorted(2**a * 3**b * 5**c for a in range(32) for b in range(32) for c in range(32))
    def nthUglyNumber(self, n: int) -> int:
        return self.ugly[n-1]
```
