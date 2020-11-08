+++
title = "72 - Edit Distance"
date = 2020-05-31T17:58:00+02:00
lastmod = 2020-05-31T18:00:15+02:00
tags = ["hard", "dp", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/edit-distance/)


## Problem {#problem}

```text
Given two words word1 and word2, find the minimum number of operations required to convert word1 to word2.

You have the following 3 operations permitted on a word:

Insert a character
Delete a character
Replace a character

Example 1:

Input: word1 = "horse", word2 = "ros"
Output: 3

Explanation:
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

Example 2:

Input: word1 = "intention", word2 = "execution"
Output: 5

Explanation:
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
```


## Solution {#solution}

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        dp = [[0] * (1+len(word2)) for _ in range(1+len(word1))]

        for i in range(1+len(word1)):
            dp[i][0] = i
        for j in range(1+len(word2)):
            dp[0][j] = j

        for i in range(1, 1+len(word1)):
            for j in range(1, 1+len(word2)):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j], dp[i-1][j-1], dp[i][j-1]) + 1

        return dp[-1][-1]
```
