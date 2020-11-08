+++
title = "39 - Combination Sum"
date = 2020-06-10T23:55:00+02:00
lastmod = 2020-08-17T16:44:11+02:00
tags = ["medium", "array", "backtrack", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/combination-sum/)


## Problem {#problem}

```text
Given a set of candidate numbers (candidates) (without duplicates) and a target number (target),
find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.

Example 1:

Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]

Example 2:

Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```


## Solution {#solution}

Backtracking problem.

See [Problem 40](http://alfmunny.com/leetcode-blog/posts/40-combination-sum-ii/).

```python
class Solution:
    def combinationSum(self, candidates, target):
        self.ans = []
        self.dfs(sorted(candidates), 0, [], target)
        return self.ans

    def dfs(self, candidates, index, path, target):
        if target == 0:
            self.ans.append(list(path))

        for i in range(index, len(candidates)):
            v = candidates[i]
            if v > target:
                return
            path.append(v)
            self.dfs(candidates, i, path, target-v)
            path.pop()
```
