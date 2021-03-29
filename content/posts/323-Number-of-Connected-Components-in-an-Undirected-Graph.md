+++
title = "323 - Number of Connected Components in an Undirected Graph"
date = 2020-12-23T23:49:00+01:00
lastmod = 2020-12-28T01:39:47+01:00
tags = ["medium", "dfs", "union-find"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)


## Problem {#problem}

```text
Given n nodes labeled from 0 to n - 1 and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.
Example 1:
Input: n = 5 and edges = [[0, 1], [1, 2], [3, 4]]
     0          3
     |          |
     1 --- 2    4
Output: 2
Example 2:
Input: n = 5 and edges = [[0, 1], [1, 2], [2, 3], [3, 4]]
     0           4
     |           |
     1 --- 2 --- 3
Output:  1
Note:
You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.
```


## Solution {#solution}

```python
from collections import defaultdict

class Solution():
    def ConnectedComponents(self, edges):
      graph = defaultdict(list)
      marked = {}
      for edge in edges:
          graph[edge[0]].append(edge[1])
          graph[edge[1]].append(edge[0])
          marked[edge[0]] = False
          marked[edge[1]] = False

      ans = 0
      for v in graph.keys():
          if not marked[v]:
              self.dfs(graph, v, marked)
              ans += 1
      return ans

    def dfs(self, graph, v, marked):
        marked[v] = True
        for w in graph[v]:
            if not marked[w]:
                self.dfs(graph, w, marked)

print(Solution().ConnectedComponents([[0, 1], [1, 2], [3, 4]]))
```
