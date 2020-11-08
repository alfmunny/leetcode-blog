+++
title = "338 - Counting Bits"
date = 2020-04-02T17:03:00+02:00
lastmod = 2020-05-29T19:45:09+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/counting-bits/)


## Problem {#problem}

```text
Given a non negative integer number num. For every numbers i in the range 0 ≤ i ≤ num calculate the number of 1's in their binary representation and return them as an array.

Example 1:

Input: 2
Output: [0,1,1]
Example 2:

Input: 5
Output: [0,1,1,2,1,2]
```


## Notes {#notes}

DP problem

-   States: index
-   Transition:

<!--listend-->

```text
dp[0] = 0
dp[1] = dp[1-1] + 1 = 1
dp[2] = dp[2-2] + 1 = 1
dp[3] = dp[3-2] + 1 = 2
dp[4] = dp[4-4] + 1 = 1
dp[5] = dp[5-4] + 1 = 2
dp[6] = dp[6-4] + 1 = 2
dp[7] = dp[7-4] + 1 = 3
dp[8] = dp[8-8] + 1 = 1
dp[9] = dp[9-8] + 1 = 2
dp[i] = dp[i - log_2 (i)] + 1

A trick using bit manipulation:

8 -> 1000
9 -> 1001
10 -> 1010

9 & 8 -> 1001 & 1000 -> 1000 dp[8] + 1  = 2
10 & 9 -> 1010 & 1001 -> 1000 dp[8] + 1 = 2
11 & 10 -> 1011 & 1010 -> 1010 dp[10] + 1 = 3
12 & 11 -> 1100 & 1011 -> 1000 dp[8] + 1 = 2

dp[i] = dp[i & (i-1)] + 1
```


## Solution {#solution}


### Solution 1: DP {#solution-1-dp}

```python
class Solution:
    def countBits(self, num):
        offset = 1
        dp = [0] * (num + 1)
        for i in range(1, num + 1):
            if offset * 2 == i:
                offset *= 2
            dp[i] = dp[i - offset] + 1
        return dp
```


### Solution 2: Bit manipulation on couting bits {#solution-2-bit-manipulation-on-couting-bits}

```python
class Solution:
    def countBits(self, num):
        dp = [0] * (num + 1)
        for i in range(1, num + 1):
            dp[i] = dp[i & (i - 1)] + 1
        return dp
```


### Solution 3: {#solution-3}

```python
class Solution(object):
    def countBits(self, num):
        res=[0]
        while len(res)<=num:
            res+=[i+1 for i in res]
        return res[:num+1]
```


### Solution 4: {#solution-4}

```python
class Solution:
    def countBits(self, num):
        dp = [0] * (num + 1)
        for i in range(1, num+1):
            if not i % 2:
                dp[i] = dp[i >> 1]
            else:
                dp[i] = dp[i >> 1] + 1

        return dp[num]
```
