+++
title = "96 - Unique Binary Search Trees"
date = 2020-03-30T15:17:00+02:00
lastmod = 2020-03-30T15:18:52+02:00
tags = ["medium", "tree", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/unique-binary-search-trees/)


## Problem {#problem}

```text
Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

Example:

Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```


## Notes {#notes}


### Solution 1: DP {#solution-1-dp}

In this dp problem, the hard part is to figure out the transition.

-   States: n
-   Transition:

    Some intuition:

    ```text
    assume dp[0] = 1
    dp[1] = dp[0]*dp[0]
    dp[2] = dp[0]*dp[1] + dp[0]*dp[1]
    dp[3] = dp[0]*dp[2] + dp[1]*dp[1] + dp[2]*dp[0]
    dp[4] = dp[0]*dp[3] + dp[1]*dp[2] + dp[2]*dp[1] + dp[3]*dp[0]
    dp[5] = dp[0]*dp[4] + dp[1]*dp[3] + dp[2]*dp[2] + dp[3]*dp[1] + dp[4]*dp[0]
    dp[6] = dp[0]*dp[5] + dp[1]*dp[4] + dp[2]*dp[3] + dp[3]*dp[2] + dp[4]*dp[1] + dp[5]*dp[0]
    ```

    ```python
    for i in range(1, n+1):
        for j in range(0, i):
            dp[i] += dp[j]*dp[i-1-j]
    ```

-   Base case:
    dp[0] = 1


### Solution 2: Catalan Number {#solution-2-catalan-number}

[Catalan Number](https://en.wikipedia.org/wiki/Catalan%5Fnumber)

```text
Cn = 1/(n+1)(2n n) = (2n)!/(n+1)!n!

The first Catalan numbers for n = 0, 1, 2, 3, ... are

1, 1, 2, 5, 14, 42, 132, 429, 1430, 4862, 16796, 58786, 208012,
742900, 2674440, 9694845, 35357670, 129644790, 477638700, 1767263190,
6564120420, 24466267020, 91482563640, 343059613650, 1289904147324, 4861946401452
```


## Solution {#solution}


### Solution 1: DP {#solution-1-dp}

```python
class Solution:
    def numTrees(self, n):
        if n < 1:
            return 0

        dp = [0] * (n+1)
        dp[0] = 1

        for i in range(1, n+1):
            for j in range(0, i):
                dp[i] += dp[j]*dp[i-1-j]

        return dp[n]
```


### Solutiojn 2: Catalan Number {#solutiojn-2-catalan-number}

```python
import math
class Solution:
    def numTrees(self, n):
        return math.factorial(2*n)/(math.factorial(n)*math.factorial(n+1))
```
