+++
title = "322 - Coin Change"
date = 2020-03-28T02:17:00+01:00
lastmod = 2020-03-28T02:17:21+01:00
draft = false
+++

[leetcode](https://leetcode.com/problems/coin-change/)


## Problem {#problem}

```text
You are given coins of different denominations and a total amount of money amount. Write a function to compute the fewest number of coins that you need to make up that amount. If that amount of money cannot be made up by any combination of the coins, return -1.

Example 1:

Input: coins = [1, 2, 5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
Example 2:

Input: coins = [2], amount = 3
Output: -1

Note:
You may assume that you have an infinite number of each kind of coin.
```


## Notes {#notes}

DP problem

States: amount

Transition: dp[i] = min(dp[i], dp[i-coins[j]]+1)


## Solution {#solution}

```python
class Solution:
    def coinChange(self, coins, amount):
        dp = [float('inf')] * (amount + 1)

        dp[0] = 0

        for i in range(1, amount + 1):
            for j in range(len(coins)):
                if i - coins[j] >= 0:
                    dp[i] = min(dp[i], dp[i - coins[j]] + 1)

        return dp[-1] if dp[-1] != float('inf') else -1
```
