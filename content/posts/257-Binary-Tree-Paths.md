+++
title = "257 - Binary Tree Paths"
date = 2020-11-22T16:42:00+01:00
lastmod = 2020-11-22T16:43:51+01:00
tags = ["easy", "tree", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/binary-tree-paths/)


## Problem {#problem}

```text
iven a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.

Example:

Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]

Explanation: All root-to-leaf paths are: 1->2->5, 1->3
```


## Solution {#solution}

```python
class Solution:
    def binaryTreePaths(self, root: TreeNode) -> List[str]:
        if not root:
            return []

        if not root.right and not root.left:
            return [str(root.val)]

        paths = [str(root.val) + "->" + s for s in self.binaryTreePaths(root.right) + self.binaryTreePaths(root.left)]
        return paths
```
