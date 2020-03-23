+++
title = "45 - Jump Game II"
author = ["alfmunny"]
date = 2020-03-22T00:55:00+01:00
lastmod = 2020-03-22T00:56:17+01:00
tags = ["easy", "array", "greedy", "bfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/jump-game-ii/)


## Problem {#problem}

```text
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

Example:

Input: [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
Note:

You can assume that you can always reach the last index.
```


## Notes {#notes}

Greedy problem.

1.  [begin, end], go through values in between, have one furthest reach.
2.  current index reach to end, jump once.
3.  next interval is [end, reach]


## Solution {#solution}

```python
class Solution:
    def jump(self, nums):

        jumps = 0
        curFurthest = 0
        curEnd = 0

        for i in range(len(nums) - 1):

            curFurthest = max(curFurthest, i + nums[i])

            if (i == curEnd):
                jumps += 1
                curEnd = curFurthest

        return jumps
```
