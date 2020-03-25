+++
title = "188 - Best Time to Buy and Sell Stock IV"
date = 2020-03-24T21:46:00+01:00
lastmod = 2020-03-25T17:08:58+01:00
tags = ["hard", "array", "dp", "1-fail", "stock"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/)


## Problem {#problem}

```text
Say you have an array for which the i-th element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most k transactions.

Note:
You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

Example 1:

Input: [2,4,1], k = 2
Output: 2
Explanation: Buy on day 1 (price = 2) and sell on day 2 (price = 4), profit = 4-2 = 2.

Example 2:

Input: [3,2,6,5,0,3], k = 2
Output: 7
Explanation: Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
             Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
```


## Notes {#notes}

See problem 121, 122 and 123.

Note the k.
If it is too large(>= n/2), treat it as if with infinitive transactions. We don't want to loop through a too large k.


## Solution {#solution}

```python
class Solution:
    def maxProfit(self, k, prices):
        if not prices:
            return 0

        n = len(prices)
        if k >= n//2: # treat it as infinitive transactions
            res = 0
            for i in range(1, n):
                if prices[i] > prices[i-1]:
                    res += prices[i] - prices[i-1]
            return res

        buy = [-sys.maxsize] * (k+1)
        sell = [0] * (k+1)

        for price in prices:
            for i in range(1, k+1):
                buy[i] = max(buy[i], sell[i-1]-price)
                sell[i] = max(sell[i], buy[i]+price)


        return sell[-1]
```
