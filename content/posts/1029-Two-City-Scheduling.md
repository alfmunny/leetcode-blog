+++
title = "1029 - Two City Scheduling"
date = 2020-06-03T20:30:00+02:00
lastmod = 2020-06-03T20:39:18+02:00
tags = ["easy", "array"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/two-city-scheduling/)


## Problem {#problem}

```text
There are 2N people a company is planning to interview. The cost of flying the i-th person to city A is costs[i][0], and the cost of flying the i-th person to city B is costs[i][1].

Return the minimum cost to fly every person to a city such that exactly N people arrive in each city.

Example 1:

Input: [[10,20],[30,200],[400,50],[30,20]]
Output: 110
Explanation:
The first person goes to city A for a cost of 10.
The second person goes to city A for a cost of 30.
The third person goes to city B for a cost of 50.
The fourth person goes to city B for a cost of 20.

The total minimum cost is 10 + 30 + 50 + 20 = 110 to have half the people interviewing in each city.

Note:

1 <= costs.length <= 100
It is guaranteed that costs.length is even.
1 <= costs[i][0], costs[i][1] <= 1000
```


## Solution {#solution}


### Solution 1: DP {#solution-1-dp}

```python
class Solution:
    def twoCitySchedCost(self, costs: List[List[int]]) -> int:
        N = len(costs) // 2

        dp = [[[float('inf')] * (N + 1), [float('inf')] * (N + 1)]
              for _ in range(2 * N + 1)]

        dp[0][0][0] = 0
        dp[0][1][0] = 0

        for i in range(1, 2 * N + 1):
            for k in range(1, N + 1):
                if i - k >= 0 and i - k <= N:
                    dp[i][0][k] = min(dp[i - 1][0][k - 1],
                                      dp[i - 1][1][i - k]) + costs[i - 1][0]
                    dp[i][1][k] = min(dp[i - 1][1][k - 1],
                                      dp[i - 1][0][i - k]) + costs[i - 1][1]

        return min(dp[-1][0][-1], dp[-1][1][-1])
```


### Solution 2: sort {#solution-2-sort}

```python
class Solution:
    def twoCitySchedCost(self, costs):
        sortedCosts = sorted(costs, key=lambda cost: cost[0] - cost[1])

        minCost = 0
        N = len(costs)

        for i in range(N//2):
            minCost += sortedCosts[i][0]
            minCost += sortedCosts[N//2+i][1]

        return minCost
```
