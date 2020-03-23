+++
title = "509 - Fibonacci Number"
author = ["alfmunny"]
lastmod = 2020-03-21T22:31:20+01:00
tags = ["easy", "array", "dp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/fibonacci-number/)


## Problem {#problem}

```text
The Fibonacci numbers, commonly denoted F(n) form a sequence, called the Fibonacci sequence, such that each number is the sum of the two preceding ones, starting from 0 and 1. That is,

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), for N > 1.
Given N, calculate F(N).



Example 1:

Input: 2
Output: 1
Explanation: F(2) = F(1) + F(0) = 1 + 0 = 1.
Example 2:

Input: 3
Output: 2
Explanation: F(3) = F(2) + F(1) = 1 + 1 = 2.
Example 3:

Input: 4
Output: 3
Explanation: F(4) = F(3) + F(2) = 2 + 1 = 3.
```


## Notes {#notes}

DP Problem.

**Important**:

Note how long is the dp array. It shoud be N+1, since we start with the number 0.


## Solution {#solution}

```python
class Solution(object):
    def fib(self, N):
        """
        :type N: int
        :rtype: int
        """
        if N < 2:
            return N

        dp = [0] * (N + 1)

        dp[0] = 0
        dp[1] = 1

        for i in range(2, N + 1):
            dp[i] = dp[i - 1] + dp[i - 2]

        return dp[-1]
```
