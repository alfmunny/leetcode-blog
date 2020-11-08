+++
title = "746 - Min Cost Climbing Stairs"
date = 2020-06-02T00:16:00+02:00
lastmod = 2020-06-02T00:18:12+02:00
tags = ["easy", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/min-cost-climbing-stairs/)


## Problem {#problem}

```text
On a staircase, the i-th step has some non-negative cost cost[i] assigned (0 indexed).

Once you pay the cost, you can either climb one or two steps. You need to find minimum cost to reach the top of the floor, and you can either start from the step with index 0, or the step with index 1.

Example 1:
Input: cost = [10, 15, 20]
Output: 15
Explanation: Cheapest is start on cost[1], pay that cost and go to the top.

Example 2:
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: Cheapest is start on cost[0], and only step on 1s, skipping cost[3].

Note:
cost will have a length in the range [2, 1000].
Every cost[i] will be an integer in the range [0, 999].
```


## Solution {#solution}

```python
class Solution:
    def minCostClimbingStairs(self, cost: List[int]) -> int:
        dp = [float('inf')] * len(cost)
        dp[0] = dp[1] = 0

        for i in range(2, len(cost)):
            dp[i] = min(dp[i-1]+cost[i-1], dp[i-2]+cost[i-2])
        return min(dp[-1]+cost[-1], dp[-2]+cost[-2])
```
