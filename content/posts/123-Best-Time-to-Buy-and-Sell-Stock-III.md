+++
title = "123 - Best Time to Buy and Sell Stock III"
date = 2020-03-24T18:25:00+01:00
lastmod = 2020-03-25T17:08:54+01:00
tags = ["hard", "array", "dp", "1-fail", "stock"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/)


## Problem {#problem}

```text
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:

Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.
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

A very good article about how to solve this kind of problem generally. [[Reference]​](https://labuladong.gitbook.io/algo/dong-tai-gui-hua-xi-lie/tuan-mie-gu-piao-wen-ti)

DP problem have three main sub problems:

1.  states => DP-Table
2.  states transition => Transition
3.  base cases => Padding or Initializtion

DP is also some kind of brute force method. We have to find all the states of the problem.
And we try to use the sub-states to apply the state transitions to simplify the calculation.

How many states do we have in all:

1.  number of days, n
2.  numebr of transactions, k = 2
3.  have the stock or not, 0 or 1

state[n][k][0 or 1] means:

the state at the n-th day, already k times transactions, have or have not the stock in hand.

State Transition:

1.  state[n][k][0] = max(state[n-1][k][0], state[n-1][k][1] + prices)

    state: I have no stock in hand

    It can transit from two states:

    -   I do not have stock yesterday               => state[n-1][k][0]

    -   I do have stock yesterday, and I sell it    => state[n-1][k][1] + prices

2.  state[n][k][1] = max(state[n-1][k][1], state[n-1][k-1][0] - prices)

    state: I have stock in hand

    It can transit from two states:

    -   I do have stock yesterday                   => state[n-1][k][1]

    -   I don't have stock yesterday, and I buy it  => state[n-1][k-1][1] - prices


## Solution {#solution}

```python
class Solution:
    def maxProfit(self, prices):
        max_k = 2
        dp = [ [ [0] * 2 for k in range(max_k + 1) ] for i in range(len(prices))]
        for i in range(len(prices)):
            for k in range(1, max_k + 1):
                if i == 0:
                    dp[i][k][0] = 0
                    dp[i][k][1] = -prices[i]
                else:
                    dp[i][k][0] = max(dp[i-1][k][0], dp[i-1][k][1] + prices[i])
                    dp[i][k][1] = max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i])

        return dp[-1][max_k][0]
```

Simple Version: reduce the DP-Table

We only have to maintain two 1-dimentional states.

```python
import sys
class Solution:
    def maxProfit(self, prices):
        buy = [-sys.maxsize] * 3
        sell = [0] * 3
        for price in prices:
            buy[1] = max(buy[1], sell[0]-price)
            buy[2] = max(buy[2], sell[1]-price)
            sell[1] = max(sell[1], buy[1]+price)
            sell[2] = max(sell[2], buy[2]+price)
            print(buy)
            print(sell)
        return sell[2]

print(Solution().maxProfit([3,3,5,0,0,3,1,4]))
```
