+++
title = "216 - Combination Sum III"
date = 2020-06-11T15:38:00+02:00
lastmod = 2020-06-11T15:39:38+02:00
tags = ["medium", "array", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/combination-sum-iv/submissions/)


## Problem {#problem}

```text
Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

Note:

All numbers will be positive integers.
The solution set must not contain duplicate combinations.
Example 1:

Input: k = 3, n = 7
Output: [[1,2,4]]
Example 2:

Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```


## Solution {#solution}

```python
class Solution:
    def combinationSum3(self, k: int, n: int) -> List[List[int]]:
        ans = []
        self.dfs(1, [], ans, k, n)
        return ans


    def dfs(self, index, path, ans, k, n):
        if k == 0 and n == 0:
            ans.append(list(path))
            return

        for i in range(index, 10):
            if i > n:
                return
            path.append(i)
            self.dfs(i+1, path, ans, k-1, n-i)
            path.pop()
```
