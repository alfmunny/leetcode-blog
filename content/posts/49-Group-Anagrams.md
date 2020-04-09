+++
title = "49 - Group Anagrams"
date = 2020-04-07T00:48:00+02:00
lastmod = 2020-04-07T00:49:20+02:00
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/group-anagrams/)


## Problem {#problem}

```text
Given an array of strings, group anagrams together.

Example:

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
Note:

All inputs will be in lowercase.
The order of your output does not matter.
```


## Solution {#solution}

Use the sorted string as key in hash table

```python
import collections
class Solution:
    def groupAnagrams(self, strs):
        ans = collections.defaultdict(list)
        for s in strs:
            ans[tuple(sorted(s))].append(s)
        return list(ans.values())
```

Or use the counter

```python
import collections
class Solution:
    def groupAnagrams(self, strs):
        ans = collections.defaultdict(list)
        for s in strs:
            a = [0] * 26
            for c in s:
                a[ord(c) - ord('a')] += 1
            ans[tuple(a)].append(s)
        return list(ans.values())
```
