+++
title = "91 - Decode Ways"
author = ["alfmunny"]
lastmod = 2020-03-21T22:28:56+01:00
tags = ["medium", "array", "dp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/decode-ways)


## Problem {#problem}

```text
A message containing letters from A-Z is being encoded to numbers using the following mapping:

'A' -> 1
'B' -> 2
...
'Z' -> 26
Given a non-empty string containing only digits, determine the total number of ways to decode it.

Example 1:

Input: "12"
Output: 2
Explanation: It could be decoded as "AB" (1 2) or "L" (12).
Example 2:

Input: "226"
Output: 3
Explanation: It could be decoded as "BZ" (2 26), "VF" (22 6), or "BBF" (2 2 6).
```


## Notes {#notes}

DP problem.

1.  Initialize dp array with dp[0] = 1 as padding, the rest of them are 0.
2.  Start from the first index of the string.
    1.  If dp[i] is in range 1 to 9, dp[i] = dp[i-1]. The ways of decode will not increase, if it is 0, it remains 0.
    2.  If dp[i] is in range 10 to 26, dp[i] += dp[i-1]. The ways of decode increase by one, if it is 00, it remains 0.

**Important**:

1.  Corner cases: "0" -> 0, "1002" -> 0
2.  Notice the padding


## Solution {#solution}

```python
class Solution():
    def numsDecodings(self, s):

        if not s:
          return 0

        n = len(s)

        dp = [0] * (n + 1)

        dp[0] = 1

        for i in range(1, n+1):

            if s[i-1: i] != '0':
                dp[i] = dp[i-1]

            if i != 1 and '10' <= s[i-2:i] <= '26':
                dp[i] += dp[i-2]

        return dp[-1]
```
