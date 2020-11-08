+++
title = "207 - Course Schedule"
date = 2020-05-29T19:57:00+02:00
lastmod = 2020-05-29T20:42:57+02:00
tags = ["medium", "graph", "dfs", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/course-schedule/)


## Problem {#problem}

```text
There are a total of numCourses courses you have to take, labeled from 0 to numCourses-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?

Example 1:

Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take.
             To take course 1 you should have finished course 0. So it is possible.

Example 2:

Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take.
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```


## Solution {#solution}


### Solution 1: DAG with DFS {#solution-1-dag-with-dfs}

```python
class Solution:
    def canFinish(self, numCourses, prerequisites):
        self.hasCycle = False
        self.adj = [[] for _ in range(numCourses)]
        self.marked = [0] * numCourses
        self.stack = [0] * numCourses

        for pre in prerequisite:
            v, w = pre
            adj[v].append(w)

        for v in range(numCourses):
            if not self.marked[v]:
                self.dfs(v)

        return not self.hasCycle

    def dfs(self, v):
        self.marked[v] = 1
        self.stack[v] = 1

        for w in self.adj[v]:
            if self.hasCycle:
                return
            elif not self.marked[w]:
                self.dfs(w)
            elif self.stack[w]:
                self.hasCycle = True
```


### Solution 2: Topological Sort {#solution-2-topological-sort}

If a graph has a topological sort order, there is no cycle.

```python
class Solution:
    def canFinish(self, numCourses, prerequisites):
        adj = [[] for _ in range(numCourses)]
        degree = [0] * numCourses

        for pre in prerequisites:
            v, w = pre
            adj[w].append(v)
            degree[v] += 1

        q = [v for v in range(numCourses) if not degree[v]]
        order = []

        while q:
            v = q.pop(0)
            order.append(v)
            for w in adj[v]:
                degree[w] -= 1
                if not degree[w]:
                    q.append(w)

        return len(order) == numCourses
```
