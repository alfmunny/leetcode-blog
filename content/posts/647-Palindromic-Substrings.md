+++
title = "647 - Palindromic Substrings"
lastmod = 2020-03-31T23:41:02+02:00
tags = ["medium", "array", "dp", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/palindromic-substrings/)


## Problem {#problem}

```text

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

Example 1:

Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".


Example 2:

Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".

Note:

The input string length won't exceed 1000.
```


## Notes {#notes}

DP problem

-   States:

    left\_index, right\_index, mark if `s[left_index, right_index+1]` is palindromic

-   Transition:

    ```text
    if s[l] == s[r]: # mark it only when both ends are same values

    dp[l][r] = 1 if r == l              # if only one element
    dp[l][r] = 1 if r+1 == l            # if only two elements
    dp[l][r] = 1 if dp[l+1][r+1] = 1    # if the string in between is palindromic

    results = results + 1
    ```

-   Base case:

    initialize dp[i][j] = 0


## Solution {#solution}

```python
class Solution:
    def countSubstrings(self, s):
        dp = [[0] * len(s) for i in range(len(s))]
        res = 0
        for r in range(len(s)):
            for l in range(r+1):
                if s[r] == s[l]:
                    if r == l or r+1 == l or dp[l+1][r-1] == 1:
                        dp[l][r] = 1
                        res += 1
        return res
print(Solution().countSubstrings("aba"))
```
