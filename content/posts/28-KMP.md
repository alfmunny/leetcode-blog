+++
title = "28 - Implement strStr() (KMP Algorithm)"
date = 2020-04-29T21:42:00+02:00
lastmod = 2020-04-29T21:43:01+02:00
tags = ["hard", "string", "kmp"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/implement-strstr/)


## Problem {#problem}

```text
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:

Input: haystack = "hello", needle = "ll"
Output: 2
Example 2:

Input: haystack = "aaaaa", needle = "bba"
Output: -1
```


## Solution {#solution}

[KMP tutorial](https://labuladong.gitbook.io/algo/dong-tai-gui-hua-xi-lie/dong-tai-gui-hua-zhi-kmp-zi-fu-pi-pei-suan-fa)

```python
class Solution:
    def __init__(self, pat):
        self.pat = pat
        self.dp = []
        self.KMP(self.pat)

    def KMP(self, pat):

        M = len(pat)
        self.dp = [[0] * 256 for _ in range(M)]
        self.dp[0][ord(pat[0])] = 1
        X = 0

        for j in range(1, M):
            for c in range(256):
                if ord(pat[j]) == c:
                    self.dp[j][c] = j + 1
                else:
                    self.dp[j][c] = self.dp[X][c]

            X = self.dp[X][ord(pat[j])]

    def search(self, txt):
        M = len(self.pat)
        N = len(txt)
        s = 0

        for i in range(N):
            s = self.dp[s][ord(txt[i])]
            if s == M:
                return i - M + 1
        return -1

sol = Solution("ababc")

print(sol.search("ababdabababc"))
```
