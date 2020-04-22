+++
title = "46 - Permutations"
date = 2020-04-19T02:11:00+02:00
lastmod = 2020-04-19T02:11:46+02:00
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
