+++
title = "863 - All Nodes Distance K in Binary Tree"
date = 2020-12-28T00:06:00+01:00
lastmod = 2020-12-28T00:09:58+01:00
tags = ["tree", "bfs", "graph", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/all-nodes-distance-k-in-binary-tree/)


## Problem {#problem}

```text
We are given a binary tree (with root node root), a target node, and an integer value K.

Return a list of the values of all nodes that have a distance K from the target node.  The answer can be returned in any order.



Example 1:

Input: root = [3,5,1,6,2,0,8,null,null,7,4], target = 5, K = 2

Output: [7,4,1]

Explanation:
The nodes that are a distance 2 from the target node (with value 5)
have values 7, 4, and 1.

Note:

1. The given tree is non-empty.
2. Each node in the tree has unique values 0 <= node.val <= 500.
3. The target node is a node in the tree.
4. 0 <= K <= 1000.
```


## Solution {#solution}

BFS

1.  Build a graph. Connet the parent and child in both directions.
2.  Start BFS search from the target value, with step of K.

In K step, the element in the new level are the answer.

```python
class Solution:
    def distanceK(self, root: TreeNode, target: TreeNode, K: int) -> List[int]:

        graph = defaultdict(list)

        self.connect(graph, root, root.left)
        self.connect(graph, root, root.right)
        level = [target.val]
        marked = set(level)
        for i in range(K):
            new_level = []
            for x in level:
                for w in graph[x]:
                    if w not in marked:
                        new_level.append(w)
            level = new_level
            marked |= set(new_level)

        return level

    def connect(self, graph, parent, child):
        if parent and child:
            graph[parent.val].append(child.val)
            graph[child.val].append(parent.val)

            self.connect(graph, child, child.left)
            self.connect(graph, child, child.right)
```
