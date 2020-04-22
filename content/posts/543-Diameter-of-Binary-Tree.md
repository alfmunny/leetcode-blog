+++
title = "543 - Diameter of Binary Tree"
date = 2020-04-11T23:58:00+02:00
lastmod = 2020-04-12T00:29:46+02:00
tags = ["easy", "tree", "recursive", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/diameter-of-binary-tree/)


## Problem {#problem}

```text
Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:
Given a binary tree
          1
         / \
        2   3
       / \
      4   5
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.
```


## Solution {#solution}

```python
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        if not root:
            return 0
        elif not root.right and not root.left:
            return 0
        elif not root.right:
            return max(self.diameterOfBinaryTree(root.left),
                       1 + self.height(root.left))
        elif not root.left:
            return max(self.diameterOfBinaryTree(root.right),
                       1 + self.height(root.right))
        else:
            return max(self.diameterOfBinaryTree(root.right),
                       self.diameterOfBinaryTree(root.left),
                       self.height(root.left) + self.height(root.right) + 2)

    def height(self, root):

        if not root:
            return 0
        if not root.right and not root.left:
            return 0

        return 1 + max(self.height(root.left), self.height(root.right))
```

```python
class Solution:
    def diameterOfBinaryTree(self, root):
        self.ans = 0

        def depth(node):
            if not node:
                return 0
            r = depth(node.right)
            l = depth(node.left)
            self.ans = max(self.ans, r+l)
            return 1 + max(r, l)
        depth(root)
        return self.ans
```
