+++
title = "263 - Ugly Number"
date = 2020-06-27T23:54:00+02:00
lastmod = 2020-06-27T23:55:14+02:00
tags = ["medium", "array", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/ugly-number-ii/)


## Problem {#problem}

```text
Write a program to check whether a given number is an ugly number.

Ugly numbers are positive numbers whose prime factors only include 2, 3, 5.

Example 1:

Input: 6
Output: true
Explanation: 6 = 2 × 3

Example 2:

Input: 8
Output: true
Explanation: 8 = 2 × 2 × 2

Example 3:

Input: 14
Output: false
Explanation: 14 is not ugly since it includes another prime factor 7.
Note:

1 is typically treated as an ugly number.
Input is within the 32-bit signed integer range: [−231,  231 − 1].
```


## Solution {#solution}

```python
class Solution:
    def isUgly(self, num: int) -> bool:
        if num <= 0:
            return False

        while num != 1:
            tmp = num
            for n in [2, 3, 5]:
                if num % n == 0:
                    num //= n
            if tmp == num:
                return False
        return True
```
