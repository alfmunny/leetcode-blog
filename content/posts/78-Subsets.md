+++
title = "78 - Subsets"
author = ["alfmunny"]
date = 2020-03-07T23:59:00+01:00
lastmod = 2020-03-14T10:16:43+01:00
tags = ["medium", "array", "backtrack", "dfs"]
categories = ["leetcode"]
draft = false
+++

## Problem {#problem}

[leetcode](https://leetcode.com/problems/subsets/)

```text
Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

Example:

Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```


## Notes {#notes}

Three strategies to solve a subset problem:

Recursion, Backtracking, Bitmask


### Recursion {#recursion}

Iterative version:

```text
Start from empty array [[]].

Step 1: Take 1 into consideration, and add 1 to existing array [[], [1]]

Step 2: Take 2 into consideration, and add 2 to existing array [[], [1], [2], [1, 2]]

Step 3: Take 3 into consideration, and add 3 to existing array [[], [1], [2], [1, 2], [3], [1, 3], [2, 3], [1, 2, 3]]
```

DFS version:

```text
[[]]
[[], [1]],
[[], [1], [1, 2]]
[[], [1], [1, 2], [1, 2, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3]]
[[], [1], [1, 2], [1, 2, 3], [1, 3], [2], [2, 3], [3]]
```


### Backtrack {#backtrack}

Backtrack needs to know how many steps it shoud take to end.

```text
[1, 2, 3]

Step 1: subsets of length 0: [[]]
Step 2: subsets of length 1: [[1], [2], [3]]
Step 3: subsets of length 2: [[1, 2], [2, 3], [1, 3]]
Step 4: subsets of length 3: [[1, 2, 3]]
```


### Bitmask {#bitmask}

> The idea is that we map each subset to a bitmask of length n,
> where 1 on the ith position in bitmask means the presence of nums[i] in the subset,
> and 0 means its absence.

[1, 2, 3]

```text
[0, 0, 0] -> []
[0, 0, 1] -> [3]
[0, 1, 0] -> [2]
[1, 0, 0] -> [1]
[1, 0, 1] -> [1, 3]
[0, 1, 1] -> [2, 3]
[1, 1, 0] -> [1, 2]
[1, 1, 1] -> [1, 2, 3]
```


## Solution {#solution}


### Solution 1: dfs (recursion) {#solution-1-dfs--recursion}

```python
class Solution(object):
    def subsets(self, nums):
        res = []
        self.dfs(sorted(nums), 0, [], res)
        return res

    def dfs(self, nums, index, path, res):
        res.append(path)
        for i in range(index, len(nums)):
            self.dfs(nums, i + 1, path + [nums[i]], res)

print(Solution().subsets([1, 2, 3]))
```


### Solution 2: iterative {#solution-2-iterative}

```python
class Solution:

    def subsets(self, nums):
        res = [[]]
        for i in sorted(nums):
            res += [item+[i] for item in res]

        return res

print(Solution().subsets([1, 2, 3]))
```


### Solution 3: backtrack {#solution-3-backtrack}

```python

class Solution(object):

    def subsets(self, nums):
        output = []
        for k in range(0, len(nums)+1):
            temp = []
            self.backtrack(0, k, nums, temp, output)

        return output

    def backtrack(self, begin, length, nums, temp, output):

        if length == len(temp):
            output.append(temp[:])

        for i in range(begin, len(nums)):
            temp.append(nums[i])
            self.backtrack(i+1, length, nums, temp, output)
            temp.pop()


print(Solution().subsets([1, 2, 3]))
```


### Solution 4: bitmask {#solution-4-bitmask}

```python

class Solution():
  def subsets(self, nums):
    n = len(nums)
    output = []
    for i in range(2**n, 2**(n+1)):
      bitmask = bin(i)[3:]
      output.append([nums[i] for i in range(n) if bitmask[i] == '1' ])

    return output
```
