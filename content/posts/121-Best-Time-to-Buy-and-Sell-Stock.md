+++
title = "121 - Best Time to Buy and Sell Stock"
date = 2020-03-24T12:13:00+01:00
lastmod = 2020-03-25T17:08:47+01:00
tags = ["easy", "array", "1-pass", "stock"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)


## Problem {#problem}

```text
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Note that you cannot sell a stock before you buy one.

Example 1:

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.

Example 2:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```


## Notes {#notes}

Mark the minPrice and the minProfit


## Solution {#solution}

```python
class Solution:
    def maxProfit(self, prices):
        if not prices:
            return 0

        minPrice = prices[0]
        maxProfit = 0

        for price in prices:
            if price < minPrice:
                minPrice = price
            if price - minPrice > maxProfit:
                maxProfit = price - minPrice
        return maxProfit
```
