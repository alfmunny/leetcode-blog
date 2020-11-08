+++
title = "46 - Permutations"
date = 2020-04-19T02:11:00+02:00
lastmod = 2020-08-02T15:19:20+02:00
tags = ["medium", "array", "backtrack", "permutation", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/permutations-ii/)


## Problem {#problem}

```text
Given a collection of distinct integers, return all possible permutations.

Example:

Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```


## Solution {#solution}


### Solution 1 {#solution-1}

```python
class Solution:
    def permute(self, nums):
        ans = []
        self.backtrack([], nums, ans)
        return ans

    def backtrack(self, path, nums, ans):
        if not nums:
            ans.append(path[:])
            return
        for i, v in enumerate(nums):
            self.backtrack(path+[v], nums[:i]+nums[i+1:], ans)
```


### Solution 2 {#solution-2}

```python
class Solution:
    def permute(self, nums: List[int]) -> List[List[int]]:
        ans = []
        marked = [False] * len(nums)
        self.dfs(nums, [], marked, ans)
        return ans

    def dfs(self, nums, path, marked, ans):
        if len(path) == len(nums):
            ans.append(list(path))
            return

        for i, n in enumerate(nums):
            if marked[i]:
                continue
            marked[i] = True
            path.append(n)
            self.dfs(nums, path, marked, ans)
            path.pop()
            marked[i] = False
```
