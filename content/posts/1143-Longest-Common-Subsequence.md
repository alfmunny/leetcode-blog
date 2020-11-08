+++
title = "1143 - Longest Common Subsequence"
date = 2020-04-27T14:49:00+02:00
lastmod = 2020-04-28T21:34:06+02:00
tags = ["medium", "string", "dp", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/longest-common-subsequence/)


## Problem {#problem}

```text
Given two strings text1 and text2, return the length of their longest common subsequence.

A subsequence of a string is a new string generated from the original string with some characters(can be none) deleted without changing the relative order of the remaining characters.
(eg, "ace" is a subsequence of "abcde" while "aec" is not).
A common subsequence of two strings is a subsequence that is common to both strings.

If there is no common subsequence, return 0.

Example 1:

Input: text1 = "abcde", text2 = "ace"
Output: 3
Explanation: The longest common subsequence is "ace" and its length is 3.

Example 2:

Input: text1 = "abc", text2 = "abc"
Output: 3
Explanation: The longest common subsequence is "abc" and its length is 3.

Example 3:

Input: text1 = "abc", text2 = "def"
Output: 0
Explanation: There is no such common subsequence, so the result is 0.
```


## Solution {#solution}

The hardest part of this problem is to figure out what is the transition.

The current state should be determined by index i, j for each string respectively.

1.  States: dp[i][j] means the longest common subsequence for text1 til index i and text2 til index j
2.  Transition:

    if text1[i] `= text2[j]: dp[i][j] = dp[i-1][j-1]
          if text1[i] !` text2[j]: dp[i][j] = max(dp[i-1][j], dp[i][j-1])

3.  Base Case: we need padding for i = 0 and j = 0

<!--listend-->

```python
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        dp = [[0] * (len(text1) + 1) for i in range(len(text2) + 1)]

        for i in range(len(text2)):
            for j in range(len(text1)):
                if text2[i] == text1[j]:
                    dp[i + 1][j + 1] = dp[i][j] + 1
                else:
                    dp[i + 1][j + 1] = max(dp[i + 1][j], dp[i][j + 1])

        return dp[-1][-1]
```
