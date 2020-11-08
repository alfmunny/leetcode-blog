+++
title = "131 - Palindrome Partitioning"
date = 2020-08-26T00:00:00+02:00
lastmod = 2020-08-26T00:13:21+02:00
tags = ["medium", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/palindrome-partitioning/)


## Problem {#problem}

```text
Given a string s, partition s such that every substring of the partition is a palindrome.

Return all possible palindrome partitioning of s.

Example:

Input: "aab"
Output:
[
  ["aa","b"],
  ["a","a","b"]
]
```


## Solution {#solution}

```python
class Solution:
    def partition(self, s: str) -> List[List[str]]:
        ans = []
        self.dfs(s, 0, ans, [])
        return ans

    def dfs(self, s, start, ans, path):

        if start == len(s):
            ans.append(path.copy())
            return

        for i in range(start, len(s)):
            w = s[start:i+1]
            if w == w[::-1]:
                path.append(w)
                self.dfs(s, i+1, ans, path)
                path.pop()
```
