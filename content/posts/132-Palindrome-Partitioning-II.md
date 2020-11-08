+++
title = "132 - Palindrome Partitioning II"
date = 2020-08-26T01:00:00+02:00
lastmod = 2020-08-26T01:07:40+02:00
tags = ["hard", "array", "dp", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/palindrome-partitioning-ii/)


## Problem {#problem}

```text
Given a string s, partition s such that every substring of the partition is a palindrome

Return the minimum cuts needed for a palindrome partitioning of s.

Example 1:

Input: s = "aab"
Output: 1
Explanation: The palindrome partitioning ["aa","b"] could be produced using 1 cut.
Example 2:

Input: s = "a"
Output: 0
Example 3:

Input: s = "ab"
Output: 1


Constraints:

1 <= s.length <= 2000
s consists of lower-case English letters only.
```


## Solution {#solution}

If s[i:j+1] is a palindrome, and if we know s[0:i] has a minCut of X, then we know minCut to for s[0:j+1] is not greater than X+1.

```python
class Solution:
    def minCut(self, s: str) -> int:
        cut = [x for x in range(-1, len(s))]
        for i in range(len(s)):
            for j in range(i, len(s)):
                if s[i:j+1] == s[i:j+1][::-1]:
                    cut[j+1] = min(cut[j+1], cut[i]+1)

        return cut[-1]
```
