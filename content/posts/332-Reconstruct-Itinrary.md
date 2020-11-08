+++
title = "332 - Reconstruct Itinrary"
date = 2020-06-29T23:40:00+02:00
lastmod = 2020-06-29T23:50:10+02:00
tags = ["medium", "graph", "dfs", "backtrack", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/reconstruct-itinerary/)


## Problem {#problem}

```text
Given a list of airline tickets represented by pairs of departure and arrival airports [from, to], reconstruct the itinerary in order. All of the tickets belong to a man who departs from JFK. Thus, the itinerary must begin with JFK.

Note:

If there are multiple valid itineraries, you should return the itinerary that has the smallest lexical order when read as a single string. For example, the itinerary ["JFK", "LGA"] has a smaller lexical order than ["JFK", "LGB"].
All airports are represented by three capital letters (IATA code).
You may assume all tickets form at least one valid itinerary.
One must use all the tickets once and only once.

Example 1:

Input: [["MUC", "LHR"], ["JFK", "MUC"], ["SFO", "SJC"], ["LHR", "SFO"]]
Output: ["JFK", "MUC", "LHR", "SFO", "SJC"]

Example 2:

Input: [["JFK","SFO"],["JFK","ATL"],["SFO","ATL"],["ATL","JFK"],["ATL","SFO"]]
Output: ["JFK","ATL","JFK","SFO","ATL","SFO"]
Explanation: Another possible reconstruction is ["JFK","SFO","ATL","JFK","ATL","SFO"].
             But it is larger in lexical order.
```


## Solution {#solution}

Eulerian Path: a path in graph that visits every edge exactly once.

Eulerian Circuit is an Eulerian Path which starts and ends on the same vertex.

Hierholzer's algorithm:

Modify the graph dfs to backtrack the vertices if there is no other unvisited edges of that vertice.

```python
while edges[vertice]:
    dfs(edges[vertice].pop())
path.append(vertice)
```

For this problem, we have to notice the lexical order for choices during dfs.

```python
class Solution:
    def findItinerary(self, tickets: List[List[str]]) -> List[str]:
        edges = defaultdict(list)

        for v, w in sorted(tickets)[::-1]:
            edges[v] += [w]
        path = []
        self.dfs("JFK", edges, path)
        return path[::-1]

    def dfs(self, vertice, edges, path):
        while(edges[vertice]):
            self.dfs(edges[vertice].pop(), edges, path)
        path.append(vertice)
```
