+++
title = "201 - Bitwise AND of Numbers Range"
date = 2020-04-24T01:35:00+02:00
lastmod = 2020-04-24T01:42:26+02:00
tags = ["medium", "bit", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/bitwise-and-of-numbers-range/)


## Problem {#problem}

```text
Given a range [m, n] where 0 <= m <= n <= 2147483647, return the bitwise AND of all numbers in this range, inclusive.

Example 1:

Input: [5,7]
Output: 4
Example 2:

Input: [0,1]
Output: 0
```


## Solution {#solution}

m = xxx1yyyy
n = xxx01zzz

`xxx` is the parts that two numbers are the same.
We can definitly find these two numbers in the range

m' = xxx1000
n' = xxx0100

So the result will be xxx0000

The idea is the find position where the the numbers are the same.

```python
class Solution:
    def rangeBitwiseAnd(self, m, n):
        i = 0
        while m != n:
            m >>= 1
            n >>= 1
            i += 1
        return n << i
```
