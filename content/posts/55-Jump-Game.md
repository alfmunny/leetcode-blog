+++
title = "55 - Jump Game"
author = ["alfmunny"]
lastmod = 2020-03-21T22:19:29+01:00
tags = ["medium", "array", "greedy"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/jump-game/)


## Problem {#problem}

```text
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

Example 1:

Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.
Example 2:

Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
```


## Notes {#notes}

Greedy algorithm. There are 2 approaches, from head or from tail.


### Start from head {#start-from-head}

always remember the furthest reachable index.

```python
reach = max(i + nums[i], reach) if i <= reach
```


### Start from tail {#start-from-tail}

always remember the last position it can reach.

```python
lastPos = i if i + nums[i] >= lastPos
```


## Solition {#solition}


### Solution 1: start from head {#solution-1-start-from-head}

```python
class Solution():
    def canJump(self, nums):
        reach = 0

        for i in range(len(nums)):
            if i <= reach:
                reach = max(i + nums[i], reach)

        return reach >= len(nums) - 1

print(Solution().canJump([ 2,3,1,1,4 ]))
print(Solution().canJump([ 3,2,1,0,4 ] ))
```


### Solution 2: start from tail {#solution-2-start-from-tail}

```python
class Solution():
    def canJump(self, nums):
        lastPos = len(nums) - 1
        for i in reversed(range(len(nums))):
            if i + nums[i] >= lastPos:
                lastPos = i

        return lastPos == 0

print(Solution().canJump([ 2,3,1,1,4 ]))
print(Solution().canJump([ 3,2,1,0,4 ] ))
```
