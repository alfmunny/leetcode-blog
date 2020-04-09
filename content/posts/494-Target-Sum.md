+++
title = "494 - Target Sum"
date = 2020-04-04T16:24:00+02:00
lastmod = 2020-04-04T17:30:20+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/target-sum/)


## Problem {#problem}

```text
You are given a list of non-negative integers, a1, a2, ..., an, and a target, S. Now you have 2 symbols + and -. For each integer, you should choose one from + and - as its new symbol.

Find out how many ways to assign symbols to make sum of integers equal to target S.

Example 1:
Input: nums is [1, 1, 1, 1, 1], S is 3.
Output: 5
Explanation:

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

There are 5 ways to assign symbols to make the sum of nums be target 3.
Note:
The length of the given array is positive and will not exceed 20.
The sum of elements in the given array will not exceed 1000.
Your output answer is guaranteed to be fitted in a 32-bit integer.
```


## Solution {#solution}

DP problem. The hardest part of this problem is to find the states.

What states do we have to calculate the current result, which is the number of ways of reaching the target.

-   States:

    -   index: how many different numbers -> n
    -   sum: how many different possible sums -> [-sum(nums), +sum(nums)]

    The tricky part is how you present the range of sum in an array.

    You have to add an offest as large as the sum(nums) to shift the range into the positive side.

    So it becomes [0, 2sum(nums)]

    For example:

    [1, 1, 1, 1, 1], you have a range of [-5, 5].

    -5, -4, -3, -2, -1, 0, 1, 2, 3, 4, 5

    Add an offset of sum = 5

    0,  1,  2,  3,  4, 5, 6, 7, 8, 9, 10  -> 11 numbers

    dp should have a length of 2sum(nums) + 1

-   Transition:

We need all the sum values of the previous number to calculate the current one.

```python
for j in range(2sum+1):
    if dp[i-1][j] > 0: # only check the ones, which have been reached
      if j+nums[i] < 2sum + 1: # sign + to the current number, we transit from j to j+nums[i]
        dp[i][j+nums[i]] += dp[i-1][j]
      if j-nums[i] >= 0: # sign + to the current number, we transit from j to j-nums[i]
        dp[i][j-nums[i]] += dp[i-1][j]
```

-   Base case:

We start from the offset.

```python
# the first number with symbols
dp[0][offset+nums[0]] +=1
dp[0][offset-nums[0]] +=1
```

**Important**:
You have to use += 1, not only = 1, because the number can be 0.

For exmaple: we take sum = 5
When the first number is 1 (not 0):

```python
d[0][0+sum + 1] += 1 -> dp[0][6] = 1
d[0][0+sum - 1] += 1 -> dp[0][4] = 1
```

It means:

there is one ways to reach 1 (6 - offset)

there is one ways to reach -1 (4 - offset)

When the first number is 0:

```python
d[0][0+sum + 1] += 1 -> dp[0][5] = 1
d[0][0+sum - 1] += 1 -> dp[0][5] = 2
```

It means there are 2 ways to reach 0 (5 - offset)


### Solution 1: 2D - DP {#solution-1-2d-dp}

```python
class Solution():
    def findTargetSumWays(self, nums, S):
        l = len(nums)
        n = 2 * sum(nums) + 1
        offset = sum(nums)

        dp = [[0] * n for i in nums]

        if not nums:
            return 0

        # base case
        dp[0][offset - nums[0]] += 1
        dp[0][offset + nums[0]] += 1

        for i in range(1, len(nums)):
            for j in range(n):
                if dp[i-1][j] > 0:
                    if j + nums[i] < n:
                        dp[i][j + nums[i]] += dp[i-1][j]
                    if j - nums[i] >= 0:
                        dp[i][j - nums[i]] += dp[i-1][j]

        return dp[-1][offset + S]


print(Solution().findTargetSumWays([1, 1, 1, 1, 1], 3))
```

Time: O(l\*n)
Space: O(l\*n)


### Solution 2: 1D - DP {#solution-2-1d-dp}

We notice that, to calculate the dp array at the current index, we only have to know one previous row.

So we only have to maintain two dp arrays to record previous values and current values respectly.

```python
class Solution:
    def findTargetSumWays(self, nums, S):
        if not nums:
            return 0
        l = len(nums)
        n = 2 * sum(nums) + 1
        offset = sum(nums)
        dp = [[0] * n for i in nums]

        dp[0][offset + nums[0]] += 1
        dp[0][offset - nums[0]] += 1

        for i in range(1, l):
            for j in range(n):
                if dp[i - 1][j] > 0:
                    if dp[i - 1][j] < n:
                        dp[i][j + nums[i]] += dp[i - 1][j]
                    if dp[i - 1][j] >= 0:
                        dp[i][j - nums[i]] += dp[i - 1][j]

        return dp[-1][offset + S]

print(Solution().findTargetSumWays([1, 1, 1, 1, 1], 3))
```
