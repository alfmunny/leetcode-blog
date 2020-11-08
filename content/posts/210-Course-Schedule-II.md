+++
title = "210 - Course Schedule II"
date = 2020-05-29T20:45:00+02:00
lastmod = 2020-06-07T14:03:02+02:00
tags = ["medium", "graph", "bfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/course-schedule-ii/)


## Problem {#problem}

```text
There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

Example 1:

Input: 2, [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished
             course 0. So the correct course order is [0,1] .
Example 2:

Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```


## Solution {#solution}

Topological sort.

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
