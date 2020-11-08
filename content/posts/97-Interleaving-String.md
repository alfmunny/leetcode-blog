+++
title = "97 - Interleaving String"
date = 2020-08-18T15:15:00+02:00
lastmod = 2020-08-18T15:15:38+02:00
tags = ["hard", "dp", "1-pass", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/interleaving-string/)


## Problem {#problem}

```text
Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

Example 1:

Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
Example 2:

Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
```


## Solution {#solution}

DP problem.

Imagin you have a matrix with s1 as its row and s2 as its column.

You have to find a path from upper left corner to bottom right corner, which consisits the s3.

So when you walk the path, you have two options:

1.  you come from left. dp[i][j] = dp[i][j-1] and s1[j-1] == s3[i+j-1]
2.  you come from above. dp[i][j] = dp[i][j-1] and s2[i-1] == s3[i+j-1]

<!--listend-->

```python
class Solution:
    def isInterleave(self, s1: str, s2: str, s3: str) -> bool:
        if len(s1) + len(s2) != len(s3):
            return False
        dp = [[False] * (len(s1)+1) for _ in range(len(s2)+1)]
        for i in range(len(s2)+1):
            for j in range(len(s1)+1):
                if not i and not j:
                    dp[i][j] = True
                elif not i:
                    dp[i][j] = dp[0][j-1] and s1[j-1] == s3[j-1]
                elif not j:
                    dp[i][j] = dp[i-1][0] and s2[i-1] == s3[i-1]
                else:
                    dp[i][j] = (dp[i-1][j] and s2[i-1] == s3[i+j-1]) or (dp[i][j-1] and s1[j-1] == s3[i+j-1])

        return dp[-1][-1]
```
