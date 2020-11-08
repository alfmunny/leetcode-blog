+++
title = "1008 - Construct Binary Search Tree from Preorder Traversal"
date = 2020-04-21T07:44:00+02:00
lastmod = 2020-05-02T00:47:59+02:00
tags = ["medium", "array", "recursive", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/construct-binary-search-tree-from-preorder-traversal/)


## Problem {#problem}

```text
Return the root node of a binary search tree that matches the given preorder traversal.

(Recall that a binary search tree is a binary tree where for every node, any descendant of node.left has a value < node.val, and any descendant of node.right has a value > node.val.  Also recall that a preorder traversal displays the value of the node first, then traverses node.left, then traverses node.right.)

Example 1:

Input: [8,5,1,7,10,12]
Output: [8,5,10,1,7,null,12]
```


## Solution {#solution}

We keep track of a low bound for the function.

We always build the right child with the low bound as the current node value.

If next value is smaller then current node value, we construct the left node.

If next value is smaller then current low bound, we construct the right node.

If next value is larger then current low bound, we jump out of the funciton.

Let the recursive jump back to the last level and repeat the same proccess

```python
class Solution:
    def bstFromPreorder(self, preorder):
        if not preorder:
            return None
        root = TreeNode(preorder[0])
        self.buildTree(root, 1, preorder, sys.maxsize)
        return root

    def buildTree(self, root, pos, preorder, rmax):
        if pos >= len(preorder) or preorder[pos] > rmax:
            return None

        if preorder[pos] < root.val:
            root.left = TreeNode(preorder[pos])
            pos = self.buildTree(root.left, pos+1, preorder, root.val - 1)

        if pos < len(preorder) and preorder[pos] <= rmax:
            root.right = TreeNode(preorder[pos])
            pos = self.buildTree(root.right, pos+1, preorder, rmax)

        return pos
```

Concise version:

```python
class Solution:
    pos = 0
    def bstFromPreorder(self, preorder, bound=float('inf')):
        if self.pos >= len(preorder) or preorder[self.pos] > bound:
            return None
        root = TreeNode(preorder[self.pos])
        self.pos += 1
        root.left = self.bstFromPreorder(preorder, root.val)
        root.right = self.bstFromPreorder(preorder, bound)
        return root
```
