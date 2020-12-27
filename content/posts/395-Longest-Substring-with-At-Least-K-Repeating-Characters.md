+++
title = "395 - Longest Substring with At Least K Repeating Characters"
date = 2020-11-21T19:03:00+01:00
lastmod = 2020-11-21T19:03:42+01:00
tags = ["medium", "dive", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/longest-substring-with-at-least-k-repeating-characters/)


## Problem {#problem}

```text
Find the length of the longest substring T of a given string (consists of lowercase letters only) such that every character in T appears no less than k times.

Example 1:

Input:
s = "aaabb", k = 3

Output:
3

The longest substring is "aaa", as 'a' is repeated 3 times.
Example 2:

Input:
s = "ababbc", k = 2

Output:
5

The longest substring is "ababb", as 'a' is repeated 2 times and 'b' is repeated 3 times
```


## Solution {#solution}

```python
class Solution:
    def longestSubstring(self, s: str, k: int) -> int:
        c = Counter(s)
        for i, v in c.items():
            if v < k:
                return max(self.longestSubstring(x, k) for x in s.split(i))
        return len(s)
```
