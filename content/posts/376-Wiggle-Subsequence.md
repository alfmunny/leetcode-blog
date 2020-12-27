+++
title = "376 - Wiggle Subsequence"
date = 2020-11-09T22:12:00+01:00
lastmod = 2020-11-09T22:14:41+01:00
tags = ["medium", "array", "dp", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/wiggle-subsequence/)


## Problem {#problem}

```text
A sequence of numbers is called a wiggle sequence if the differences between successive numbers strictly alternate between positive and negative. The first difference (if one exists) may be either positive or negative. A sequence with fewer than two elements is trivially a wiggle sequence.

For example, [1,7,4,9,2,5] is a wiggle sequence because the differences (6,-3,5,-7,3) are alternately positive and negative. In contrast, [1,4,7,2,5] and [1,7,4,5,5] are not wiggle sequences, the first because its first two differences are positive and the second because its last difference is zero.

Given a sequence of integers, return the length of the longest subsequence that is a wiggle sequence. A subsequence is obtained by deleting some number of elements (eventually, also zero) from the original sequence, leaving the remaining elements in their original order.

Example 1:

Input: [1,7,4,9,2,5]
Output: 6
Explanation: The entire sequence is a wiggle sequence.
Example 2:

Input: [1,17,5,10,13,15,10,5,16,8]
Output: 7
Explanation: There are several subsequences that achieve this length. One is [1,17,10,13,10,16,8].
Example 3:

Input: [1,2,3,4,5,6,7,8,9]
Output: 2
Follow up:
Can you do it in O(n) time?
```


## Solution {#solution}

```python
class Solution:
    def wiggleMaxLength(self, nums: List[int]) -> int:
        if len(nums) < 2:
            return len(nums)

        first_diff = 1
        dp = [1] * len(nums)
        ret = 1

        for first_diff in [1, -1]:
            dp = [1] * len(nums)
            for i in range(1, len(nums)):
                if first_diff * (nums[i] - nums[i-1]) > 0:
                    dp[i] = dp[i-1] + 1
                    first_diff *= -1
                else:
                    dp[i] = dp[i-1]

            ret = max(ret, max(dp))

        return ret
```
