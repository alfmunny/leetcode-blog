+++
title = "10 - Regular Expression Matching"
date = 2020-07-10T02:20:00+02:00
lastmod = 2020-07-10T02:22:57+02:00
tags = ["hard", "array", "dp", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/regular-expression-matching/)


## Problem {#problem}

```text
Given an input string (s) and a pattern (p), implement regular expression matching with support for '.' and '*'.

'.' Matches any single character.
'*' Matches zero or more of the preceding element.
The matching should cover the entire input string (not partial).

Note:

s could be empty and contains only lowercase letters a-z.
p could be empty and contains only lowercase letters a-z, and characters like . or *.
Example 1:

Input:
s = "aa"
p = "a"
Output: false
Explanation: "a" does not match the entire string "aa".

Example 2:

Input:
s = "aa"
p = "a*"
Output: true
Explanation: '*' means zero or more of the preceding element, 'a'. Therefore, by repeating 'a' once, it becomes "aa".

Example 3:

Input:
s = "ab"
p = ".*"
Output: true
Explanation: ".*" means "zero or more (*) of any character (.)".

Example 4:

Input:
s = "aab"
p = "c*a*b"
Output: true
Explanation: c can be repeated 0 times, a can be repeated 1 time. Therefore, it matches "aab".

Example 5:

Input:
s = "mississippi"
p = "mis*is*p*."
Output: false
```


## Solution {#solution}

```python
class Solution:
    def isMatch(self, s: str, p: str) -> bool:

        dp = [[False] * (len(s)+1) for _ in range(len(p)+1)]

        dp[0][0] = True

        for i in range(len(p)):
            if p[i] == "*" and dp[i-1][0]:
                dp[i+1][0] = True

        for i in range(len(p)):
            for j in range(len(s)):
                if p[i] == s[j]:
                    dp[i+1][j+1] = dp[i][j]
                elif p[i] == '.':
                    dp[i+1][j+1] = dp[i][j]
                elif p[i] == '*':
                    if p[i-1] != s[j] and p[i-1] != '.':
                        dp[i+1][j+1] = dp[i-1][j+1]
                    else:
                        dp[i+1][j+1] = dp[i][j+1] or dp[i+1][j] or dp[i-1][j+1]
        return dp[-1][-1]
```
