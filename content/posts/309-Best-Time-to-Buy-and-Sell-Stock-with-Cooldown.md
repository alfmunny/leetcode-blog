+++
title = "309 - Best Time to Buy and Sell Stock with Cooldown"
date = 2020-03-24T22:36:00+01:00
lastmod = 2020-03-25T17:09:01+01:00
tags = ["hard", "array", "dp", "1-fail", "stock"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown)


## Problem {#problem}

```text
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)
Example:

Input: [1,2,3,0,2]
Output: 3
Explanation: transactions = [buy, sell, cooldown, buy, sell]
```


## Notes {#notes}


## Solution {#solution}

```python
import sys
class Solution:
    def maxProfit(self, prices):
        dp_buy = -sys.maxsize
        dp_sell = 0
        dp_pre_0 = 0

        for price in prices:
            tmp = dp_sell
            dp_sell = max(dp_sell, dp_buy + price)
            dp_buy = max(dp_buy, dp_pre_0 - price)
            dp_pre_0 = tmp

        return dp_sell
```
