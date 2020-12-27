+++
title = "139 - Word Break"
date = 2020-11-30T01:29:00+01:00
lastmod = 2020-11-30T01:29:43+01:00
tags = ["medium", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/word-break-ii/)


## Problem {#problem}

```text
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.
Example 1:

Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
Example 2:

Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
Example 3:

Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```


## Solution {#solution}

```python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        memo = {}

        def dfs(index):
            if index in memo: return memo[index]
            if index >= len(s): return True

            ret = False
            for i in range(index+1, len(s)+1):
                if s[index:i] in wordDict:
                    if dfs(i):
                        ret = True
                        break

            memo[index] = ret
            return ret

        return dfs(0)
```
