+++
title = "983 - Minimum Cost For Tickets"
date = 2020-08-26T22:50:00+02:00
lastmod = 2020-08-26T23:25:45+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/minimum-cost-for-tickets/)


## Problem {#problem}

```text
In a country popular for train travel, you have planned some train travelling one year in advance.  The days of the year that you will travel is given as an array days.  Each day is an integer from 1 to 365.

Train tickets are sold in 3 different ways:

a 1-day pass is sold for costs[0] dollars;
a 7-day pass is sold for costs[1] dollars;
a 30-day pass is sold for costs[2] dollars.
The passes allow that many days of consecutive travel.  For example, if we get a 7-day pass on day 2, then we can travel for 7 days: day 2, 3, 4, 5, 6, 7, and 8.

Return the minimum number of dollars you need to travel every day in the given list of days.



Example 1:

Input: days = [1,4,6,7,8,20], costs = [2,7,15]
Output: 11
Explanation:
For example, here is one way to buy passes that lets you travel your travel plan:
On day 1, you bought a 1-day pass for costs[0] = $2, which covered day 1.
On day 3, you bought a 7-day pass for costs[1] = $7, which covered days 3, 4, ..., 9.
On day 20, you bought a 1-day pass for costs[0] = $2, which covered day 20.
In total you spent $11 and covered all the days of your travel.
Example 2:

Input: days = [1,2,3,4,5,6,7,8,9,10,30,31], costs = [2,7,15]
Output: 17
Explanation:
For example, here is one way to buy passes that lets you travel your travel plan:
On day 1, you bought a 30-day pass for costs[2] = $15 which covered days 1, 2, ..., 30.
On day 31, you bought a 1-day pass for costs[0] = $2 which covered day 31.
In total you spent $17 and covered all the days of your travel.
```


## Solution {#solution}

DP problem. dp[i] represents the min cost for ith day.

We have four options for one day.

1.  We don't travel:
    dp[i] = dp[i-1]

2.  We have to travel:

    a. buy 1-day ticket: dp[i] = dp[i-1] + costs[0]
    b. buy 7-days ticket which can cover ith day: dp[i] = min(dp[i-1], dp[i-2], dp[i-3], ... dp[i-7]) + costs[1]
    c. buy 30-days ticket which can cover ith day: dp[i] = min(dp[i-1], dp[i-2], ... dp[i-30]) + costs[2]

Important is to know, the min cost is always increasing.

So min(dp[i-1], dp[i-2]... dp[i-7]) = dp[i-7]

dp[i] = min(dp[i-1] + costs[0], dp[i-7] + costs[0], dp[i-30] + costs[0])

Note that, i-7 and i-30 might smaller than 0 in the loop. Use max(0, i-7) to avoid that.

```python
class Solution:
    def mincostTickets(self, days: List[int], costs: List[int]) -> int:
        dp = [0] * (max(days)+1)

        for i in range(1, len(dp)):
            if i not in days:
                dp[i] = dp[i-1]
            else:
                dp[i] = min(dp[i-1]+costs[0], dp[max(0, i-7)] + costs[1], dp[max(0, i-30)] + costs[2])

        return dp[-1]
```
