+++
title = "202 - Happy Number"
date = 2020-04-02T16:03:00+02:00
lastmod = 2020-04-02T16:04:18+02:00
tags = ["easy", "array", "hash", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/happy-number/)


## Problem {#problem}

```text
Write an algorithm to determine if a number is "happy".

A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle which does not include 1. Those numbers for which this process ends in 1 are happy numbers.

Example:

Input: 19
Output: true
Explanation:
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1
```


## Notes {#notes}

Hash Table


## Solution {#solution}

```python
class Solution:
    def isHappy(self, n):
        table = {}

        while n != 1:
            x = n
            n = 0
            while x != 0:
                n += (x % 10)**2
                x //= 10

            if table.get(n):
                return False
            else:
                table[n] = 1
        return True


class Solution:
    def isHappy(self, n):
        mem = set()
        while n not in mem:
            mem.add(n)
            n = sum(int(i)**2 for i in str(n))
        return n == 1
```
