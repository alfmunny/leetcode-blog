+++
title = "515 - Find Largest Value in Each Tree Row"
date = 2020-12-29T21:51:00+01:00
lastmod = 2020-12-29T22:29:38+01:00
tags = ["medium", "tree", "bfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/find-largest-value-in-each-tree-row/)


## Problem {#problem}

```text
Given the root of a binary tree, return an array of the largest value in each row of the tree (0-indexed).
```


## Solution {#solution}

```python
class Solution:
    def largestValues(self, root: TreeNode) -> List[int]:
        if not root:
            return []
        ans = []
        level = [root]
        seen = set(level)

        while level:
            new_level = []
            max_val = -float('inf')
            for node in level:
                if node:
                    if node.left:
                        new_level.append(node.left)
                    if node.right:
                        new_level.append(node.right)
                    max_val = max(max_val, node.val)
            ans.append(max_val)
            level = new_level

        return ans
```
