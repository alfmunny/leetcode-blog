+++
title = "886 - Possible Bipartition"
date = 2020-05-27T16:37:00+02:00
lastmod = 2020-05-27T16:38:15+02:00
tags = ["medium", "array", "graph", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/possible-bipartition/)


## Problem {#problem}

```text
Given a set of N people (numbered 1, 2, ..., N), we would like to split everyone into two groups of any size.

Each person may dislike some other people, and they should not go into the same group.

Formally, if dislikes[i] = [a, b], it means it is not allowed to put the people numbered a and b into the same group.

Return true if and only if it is possible to split everyone into two groups in this way.

Example 1:

Input: N = 4, dislikes = [[1,2],[1,3],[2,4]]
Output: true
Explanation: group1 [1,4], group2 [2,3]

Example 2:

Input: N = 3, dislikes = [[1,2],[1,3],[2,3]]
Output: false

Example 3:

Input: N = 5, dislikes = [[1,2],[2,3],[3,4],[4,5],[1,5]]
Output: false


Note:

1. 1 <= N <= 2000
2. 0 <= dislikes.length <= 10000
3. 1 <= dislikes[i][j] <= N
4. dislikes[i][0] < dislikes[i][1]
5. There does not exist i != j for which dislikes[i] == dislikes[j].
```


## Solution {#solution}

```python
class Solution:
    def possibleBipartition(self, N: int, dislikes):
        self.graph = [[] for _ in range(N+1)]
        self.marked = [0] * (N+1)

        for pair in dislikes:
            v, w = pair
            self.graph[v].append(w)
            self.graph[w].append(v)

        for v in range(1, N+1):
            if not self.marked[v] and not self.dfs(v, 1):
                return False
        return True

    def dfs(self, v, color):
        self.marked[v] = color
        for w in self.graph[v]:
            if not self.marked[w] and not self.dfs(w, -color):
                return False
            elif self.marked[w] == color:
                return False

        return True
```
