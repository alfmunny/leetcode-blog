+++
title = "784 - Letter Case Permutation"
date = 2020-08-19T19:45:00+02:00
lastmod = 2020-08-19T19:46:38+02:00
tags = ["medium", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/letter-case-permutation/)


## Problem {#problem}

```text
Given a string S, we can transform every letter individually to be lowercase or uppercase to create another string.

Return a list of all possible strings we could create. You can return the output  in any order.



Example 1:

Input: S = "a1b2"
Output: ["a1b2","a1B2","A1b2","A1B2"]
Example 2:

Input: S = "3z4"
Output: ["3z4","3Z4"]
Example 3:

Input: S = "12345"
Output: ["12345"]
Example 4:

Input: S = "0"
Output: ["0"]


Constraints:

S will be a string with length between 1 and 12.
S will consist only of letters or digits.
```


## Solution {#solution}

```python
class Solution:
    def letterCasePermutation(self, S: str) -> List[str]:
        ans = []
        self.dfs(S, 0, ans, [])
        return ans

    def dfs(self, S, i, ans, path):
        if i == len(S):
            ans.append(''.join(path))
            return

        self.dfs(S, i+1, ans, path + [S[i]])

        if S[i].isalpha():
            self.dfs(S, i+1, ans, path + [S[i].swapcase()])
```
