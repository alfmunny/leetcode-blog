+++
title = "438 - Find All Anagrams in a String"
date = 2020-05-18T05:08:00+02:00
lastmod = 2020-05-18T05:10:26+02:00
tags = ["medium", "array", "sliding-window", "1-fail", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/find-all-anagrams-in-a-string/)


## Problem {#problem}

```text
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

Example 1:

Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```


## Solution {#solution}

```python
from collections import defaultdict

class Solution:
    def findAllAnagrams(self, s, p):
        target, window = defaultdict(int), defaultdict(int)
        left, right = 0, 0
        match = 0
        ans = []

        for c in p:
            target[c] += 1

        while right < len(s):
            c = s[right]
            if c in target:
                window[c] += 1
                if window[c] == target[c]:
                    match += 1

            right += 1

            while right - left + 1 > len(p):
                if match == len(target):
                    ans.append(left)
                c = s[left]
                left += 1

                if c in window:
                    if window[c] == target[c]:
                        match -= 1
                    window[c] -= 1


        return ans

print(Solution().findAllAnagrams("cbaeabac", "abc"))
```
