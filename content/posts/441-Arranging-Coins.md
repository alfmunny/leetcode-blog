+++
title = "441 - Arranging Coins"
date = 2020-07-01T23:57:00+02:00
lastmod = 2020-07-01T23:58:51+02:00
tags = ["easy", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/arranging-coins/)


## Problem {#problem}

```text
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:

n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.
Example 2:

n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
```


## Solution {#solution}

```python
class Solution:
    def arrangeCoins(self, n: int) -> int:
        k = 0
        while n > 0:
            k += 1
            n -= k

        return k if not n else k - 1
```
