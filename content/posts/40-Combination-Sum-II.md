+++
title = "40 - Combination Sum II"
date = 2020-06-10T23:33:00+02:00
lastmod = 2020-06-10T23:34:01+02:00
tags = ["medium", "array", "backtrack", "dfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/combination-sum-ii/)


## Problem {#problem}

```text
Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:

Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
Example 2:

Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```


## Solution {#solution}

Backtracking problem.

Use DFS.

1.  make a choice
2.  call dfs recursive for all rest choices
3.  revert the choice

Notes:

1.  sort the candidates and avoid the duplicates
2.  return early when the target is smaller than 0

<!--listend-->

```python
class Solution:
    def combinationSum(self, candidates, target):
        self.ans = []
        candidates.sort()
        self.dfs(candidates, 0, [], target)
        return self.ans

    def dfs(self, candidates, index, path, target):
        if target < 0:
            return

        if target == 0:
            self.ans.append(list(path))

        for i in range(index, len(candidates)):
            if i > index and candidates[i] == candidates[i-1]:
                continue
            path.append(candidates[i])
            self.dfs(i+1, candidates, path, target-candidates[i])
            path.pop()
```
