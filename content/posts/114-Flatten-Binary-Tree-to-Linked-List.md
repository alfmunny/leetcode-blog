+++
title = "114 - Flatten Binary Tree to Linked List"
date = 2020-08-19T14:55:00+02:00
lastmod = 2020-08-19T15:01:48+02:00
tags = ["medium", "tree", "dfs", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/flatten-binary-tree-to-linked-list/)


## Problem {#problem}

```text
Given a binary tree, flatten it to a linked list in-place.

For example, given the following tree:

    1
   / \
  2   5
 / \   \
3   4   6
The flattened tree should look like:

1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```


## Solution {#solution}

1.  Traverse the tree in reverse preorder, the opposite of root-left-right.
2.  Save the root, and use it in the upper level.

<!--listend-->

```python
class Solution:
    def flatten(self, root: TreeNode) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        self.pre = None
        self.dfs(root)

    def dfs(self, root):

        if not root:
            return

        self.dfs(root.right)
        self.dfs(root.left)

        root.right = self.pre
        self.pre = root
        root.left = None
```
