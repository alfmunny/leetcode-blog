+++
title = "58 - Length of Last Word"
date = 2020-06-18T13:46:00+02:00
lastmod = 2020-06-18T13:51:27+02:00
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/length-of-last-word/)


## Problem {#problem}

```text
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word (last word means the last appearing word if we loop from left to right) in the string.

If the last word does not exist, return 0.

Note: A word is defined as a maximal substring consisting of non-space characters only.

Example:

Input: "Hello World"
Output: 5
```


## Solution {#solution}

```python
class Solution:
    def lengthOfLastWord(self, s: str) -> int:
        if s.split():
            return len(s.split()[-1])
        else:
            return 0
```
