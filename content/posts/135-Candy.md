+++
title = "135 - Candy"
date = 2020-11-28T01:09:00+01:00
lastmod = 2020-11-28T01:12:11+01:00
tags = ["medium", "trick", "math", "array", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/candy/)


## Problem {#problem}

```text
There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

Each child must have at least one candy.
Children with a higher rating get more candies than their neighbors.
What is the minimum candies you must give?

Example 1:

Input: [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
Example 2:

Input: [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
             The third child gets 1 candy because it satisfies the above two conditions.
```


## Solution {#solution}

```python
class Solution:
    def candy(self, ratings: List[int]) -> int:

        candy = [1] * len(ratings)

        for i in range(len(candy)-1):
            if ratings[i+1] > ratings[i]:
                candy[i+1] = candy[i] + 1

        for i in range(len(candy)-1, 0, -1):
            if ratings[i-1] > ratings[i]:
                candy[i-1] = max(candy[i]+1, candy[i-1])

        return sum(candy)
```
