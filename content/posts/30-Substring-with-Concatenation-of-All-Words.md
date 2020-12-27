+++
title = "30 - Substring with Concatenation of All Words"
date = 2020-11-30T23:23:00+01:00
lastmod = 2020-11-30T23:24:41+01:00
tags = ["hard", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/substring-with-concatenation-of-all-words/)


## Problem {#problem}

```text
You are given a string s and an array of strings words of the same length. Return all starting indices of substring(s) in s that is a concatenation of each word in words exactly once, in any order, and without any intervening characters.

You can return the answer in any order.



Example 1:

Input: s = "barfoothefoobarman", words = ["foo","bar"]
Output: [0,9]
Explanation: Substrings starting at index 0 and 9 are "barfoo" and "foobar" respectively.
The output order does not matter, returning [9,0] is fine too.
Example 2:

Input: s = "wordgoodgoodgoodbestword", words = ["word","good","best","word"]
Output: []
Example 3:

Input: s = "barfoofoobarthefoobarman", words = ["bar","foo","the"]
Output: [6,9,12]
```


## Solution {#solution}

```python
class Solution:
    def findSubstring(self, s: str, words: List[str]) -> List[int]:
        if not s or not words:
            return []
        length = len(words[0])
        total_words = len(words)
        words = Counter(words)
        ans = []
        def dfs(start, i, path):
            if len(path) == total_words:
                ans.append(start)
                return
            if i >= len(s):
                return
            w = s[i:i+length]
            if words[w]:
                words[w] -= 1
                dfs(start, i+length, path+[w])
                words[w] += 1

        for i in range(len(s)-length*total_words+1):
            dfs(i, i, [])

        return ans
```
