+++
title = "122 - Best Time to Buy and Sell Stock II"
date = 2020-03-24T15:26:00+01:00
lastmod = 2020-03-25T17:08:51+01:00
tags = ["easy", "array", "1-pass", "stock"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii)


## Problem {#problem}

```text
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:

Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.
Example 2:

Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.
Example 3:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```


## Notes {#notes}


### Solution 1 {#solution-1}

Find the valley and peak, save the local maxProfit, add it up when new valley is found.


### Solution 2 {#solution-2}

Simplify the solution 1:
we can sum up the profit when we go up step by step.


## Solution {#solution}


### Solution 1: {#solution-1}

```python
class Solution:
    def maxProfit(self, prices):
        if not prices:
            return 0

        valley = prices[0]
        maxProfit = 0
        res = 0

        for price in prices:
            if price - valley < maxProfit:
                valley = price # new valley
                res += maxProfit # add the current maxProfit
                maxProfit = 0 # reset current maxProfit
            else:
                maxProfit = price - valley # update the maxProfit when we still go up

        # remember to add the last maxProfit.
        # 1. When we are on the peak. maxProfit > 0, it should be added
        # 2. When we are in the vally, maxProfit = 0, would not affect the value
        res += maxProfit

        return res
```


### Solution 2: {#solution-2}

```python
class Solution:
    def maxProfit(self, prices):
        res = 0
        for i in range(1, len(prices)):
            if (prices[i-1] < prices[i]):
                res += prices[i] - prices[i-1]
        return res
```
