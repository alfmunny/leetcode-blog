+++
title = "516 - Longest Palindromic Subsequence"
date = 2020-08-22T12:25:00+02:00
lastmod = 2020-08-22T12:26:17+02:00
tags = ["medium", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/longest-palindromic-subsequence/)


## Problem {#problem}

```text
Given a string s, find the longest palindromic subsequence's length in s. You may assume that the maximum length of s is 1000.

Example 1:
Input:

"bbbab"
Output:
4
One possible longest palindromic subsequence is "bbbb".


Example 2:
Input:

"cbbd"
Output:
2
One possible longest palindromic subsequence is "bb".


Constraints:

1 <= s.length <= 1000
s consists only of lowercase English letters.
```


## Solution {#solution}

DP problem.

dp[i][j] represents the max value for substring from j to i.

Transition:

if s[i] == s[j]: dp[i][j] = dp[i-1][j+1] + 2
else: dp[i][j] = max(dp[i-1][j] + dp[i][j+1])

```python
class Solution:
    def longestPalindromeSubseq(self, s: str) -> int:
        dp = [[0] * len(s) for i in range(len(s))]

        for i in range(0, len(s)):
            dp[i][i] = 1
            for j in range(i-1, -1, -1):
                if s[i] == s[j]:
                    dp[i][j] = dp[i-1][j+1] + 2
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j+1])
        return dp[-1][0] if s else 0
```
