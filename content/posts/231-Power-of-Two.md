+++
title = "231 - Power of Two"
date = 2020-06-08T22:35:00+02:00
lastmod = 2020-06-08T22:36:24+02:00
tags = ["easy", "bit", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/power-of-two/)


## Problem {#problem}

```text
Given an integer, write a function to determine if it is a power of two.

Example 1:

Input: 1
Output: true
Explanation: 20 = 1

Example 2:

Input: 16
Output: true
Explanation: 24 = 16

Example 3:

Input: 218
Output: false
```


## Solution {#solution}


### Solution 1: Straight forward {#solution-1-straight-forward}

```python
class Solution:
    def powerOfTwo(self, n):
        while n != 1:
            if n % 2:
                return False
            n //= 2

        return True
```


### Solution 2: Bit manipulation {#solution-2-bit-manipulation}

power of two:
n     = 1000000
n - 1 = 111111
n & (n-1) == 0

Note: n can not be 0

```python
class Solution:
    def powerOfTwo(self, n):
        return n and not (n & n-1)
```
