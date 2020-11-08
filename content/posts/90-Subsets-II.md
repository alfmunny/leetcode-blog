+++
title = "90 - Subsets II"
date = 2020-06-17T23:45:00+02:00
lastmod = 2020-06-17T23:46:33+02:00
tags = ["medium", "array", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/subsets-ii/)


## Problem {#problem}

```text
Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```


## Solution {#solution}

```python
class Solution:
    def subsetsWithDup(self, nums: List[int]) -> List[List[int]]:
        ans = []
        marked = [False] * len(nums)

        self.dfs(sorted(nums), 0, [], ans, marked)

        return ans

    def dfs(self, nums, index, path, ans, marked):
        ans.append(list(path))
        for i in range(index, len(nums)):
            if i > 0 and nums[i] == nums[i-1] and not marked[i-1]:
                continue

            marked[i] = True
            path.append(nums[i])
            self.dfs(nums, i+1, path, ans, marked)
            path.pop()
            marked[i] = False
```
