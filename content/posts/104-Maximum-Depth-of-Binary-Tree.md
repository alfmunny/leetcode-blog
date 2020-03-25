+++
title = "104 - Maximum Depth of Binary Tree"
date = 2020-03-25T17:16:00+01:00
lastmod = 2020-03-25T17:17:31+01:00
tags = ["easy", "tree", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/maximum-depth-of-binary-tree/)


## Problem {#problem}

```text
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```


## Notes {#notes}

Recursion is your friend!


## Solution {#solution}

```python
class Solution:
    def maxDepth(self, root):
        return 1 + max(self.maxDepth(root.right), self.maxDepth(root.left)) if root else 0
```
