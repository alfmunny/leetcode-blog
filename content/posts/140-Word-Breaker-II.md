+++
title = "140 - Word Breaker II"
date = 2020-11-30T01:13:00+01:00
lastmod = 2020-11-30T01:15:05+01:00
tags = ["hard", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/word-break-ii/)


## Problem {#problem}

```text
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.
Example 1:

Input:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
Output:
[
  "cats and dog",
  "cat sand dog"
]
Example 2:

Input:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
Output:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
Explanation: Note that you are allowed to reuse a dictionary word.
Example 3:

Input:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
Output:
[]
```


## Solution {#solution}

```python
class Solution(object):
    def wordBreak(self, s, wordDict):
        return self.dfs(s, set(wordDict), 0, {})

    def dfs(self, s, wordDict, start, memo):

        if start >= len(s): return [""]
        if start in memo: return memo[start]

        ans = []
        for i in range(start+1, len(s)+1):
            w = s[start:i]
            if w in wordDict:
                ans += [" ".join([w, x]) if x else w for x in self.dfs(s, wordDict, i, memo)]

        memo[start] = ans
        return ans
```
