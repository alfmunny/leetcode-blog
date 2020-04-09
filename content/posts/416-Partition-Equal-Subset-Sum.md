+++
title = "416 - Partition Equal Subset Sum"
date = 2020-04-05T21:20:00+02:00
lastmod = 2020-04-08T11:26:24+02:00
tags = ["medium", "array", "dp", "bit", "1-hint", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/partition-equal-subset-sum/)


## Problem {#problem}

```text
Given a non-empty array containing only positive integers, find if the array can be partitioned into two subsets such that the sum of elements in both subsets is equal.

Note:

Each of the array element will not exceed 100.
The array size will not exceed 200.


Example 1:

Input: [1, 5, 11, 5]

Output: true

Explanation: The array can be partitioned as [1, 5, 5] and [11].


Example 2:

Input: [1, 2, 3, 5]

Output: false

Explanation: The array cannot be partitioned into equal sum subsets.
```


## Solution {#solution}

DP problem, it is similar to problem 494 Target Sum.

Maintain a dp table: dp[i][sum]. Don't forget to the offset.

Transition:
dp[i][j-nums[i]] += dp[i-1][j]
dp[i][j+nums[i]] += dp[i-1][j]

When the transition is only depend on the last row, usually you always can transform the dp table to 1 dimensional.


### Solution 1: 1D-DP {#solution-1-1d-dp}

```python
class Solution:
    def canPartition(slef, nums):
        nums_sum = sum(nums)
        if nums_sum % 2 != 0:
            return False

        target = nums_sum//2
        n = target + 1

        dp = [False] * n
        dp[0] = True
        for i in range(len(nums)):
            for j in reversed(range(nums[i], n)):
                dp[j] = dp[j-nums[i]] or dp[j]
                if dp[target]:
                    return True
        return dp[target]
```

Time: O(len(nums)\*sum(nums))

Space: O(len(nums)\*sum(nums))


### Solution 2: Bit manipulation for maintaning the dp table {#solution-2-bit-manipulation-for-maintaning-the-dp-table}

```python
class Solution:
    def canPartition(self, nums):
        s = sum(nums)
        if s%2 != 0:
            return False

        bits = 1
        for i in nums:
            bits |= bits << i

        return (bits >> (s//2)) & 1 == 1
```

Time: O(n)

Space: O(1) maybe, depends on the sum of the array, the bits can be longer
