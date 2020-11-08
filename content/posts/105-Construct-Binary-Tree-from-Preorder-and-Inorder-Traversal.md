+++
title = "105 - Construct Binary Tree from Preorder and Inorder Traversal"
date = 2020-05-02T00:21:00+02:00
lastmod = 2020-05-02T00:29:44+02:00
tags = ["medium", "tree", "recursion", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)


## Problem {#problem}

```text
Given preorder and inorder traversal of a tree, construct the binary tree.

Note:
You may assume that duplicates do not exist in the tree.

For example, given

preorder = [3,9,20,15,7]
inorder = [9,3,15,20,7]
Return the following binary tree:

    3
   / \
  9  20
    /  \
   15   7
```


## Solution {#solution}

1.  The first node of the preorder is always the root.
2.  Find the root in the inorder array, split it there. The left part are all the nodes in left branch. the right part in the right branch.
3.  Repeat it recursively. Note that we should always pop the first node of preorder as current root(solution 1). All keep a global index as shown(solution 2).

Simple Version:

It uses a lot resources

1.  index() operation is also not O(1).
2.  inorder[:split] copies the sub array to the next level recursion.

<!--listend-->

```python
class Solution:
    def buildTree(self, preorder, inorder):
        if inorder:
            node = TreeNode(preorder.pop(0))
            split = inorder.index(node.val)
            node.left = self.buildTree(preorder, inorder[:split])
            ndoe.right = self.buildTree(preorder, inorder[split+1:])
            return node
```

Optimized Version:

1.  use a map instead of index() operation
2.  pass the index instead of the sub array it self

<!--listend-->

```python
class Solution(object):
    def __init__(self):
        self.map = {}

    def buildTree(self, preorder, inorder):
        for i, val in enumerate(inorder):
            self.map[val] = i

        return self.recursive(0, len(preorder) - 1, preorder, inorder)

    def recursive(self, start, end, preorder, inorder):
        if (start > end):
            return None

        node = TreeNode(preorder.pop(0))

        split = self.map[node.val]

        node.left = self.recursive(start, split - 1, preorder, inorder)
        node.right = self.recursive(split + 1, end, preorder, inorder)

        return node
```
