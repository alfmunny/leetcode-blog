+++
title = "77 - Combinations"
date = 2020-06-12T17:56:00+02:00
lastmod = 2020-06-12T17:58:04+02:00
tags = ["medium", "array", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/combination-sum-ii/)


## Problem {#problem}

```text
Share
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

Example:

Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```


## Solution {#solution}

```python
class Solution:
    def combine(self, n: int, k: int) -> List[List[int]]:
        ans = []
        self.dfs(1, n, k, [], ans)
        return ans

    def dfs(self, index, n, k, path, ans):
        if k == 0:
            ans.append(list(path))
            return

        for i in range(index, n+1):
            path.append(i)
            self.dfs(i+1, n, k-1, path, ans)
            path.pop()
```
