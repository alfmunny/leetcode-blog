+++
title = "98 - Validate Binary Search Tree"
date = 2020-05-02T17:19:00+02:00
lastmod = 2020-05-02T17:19:14+02:00
tags = ["medium", "tree", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/validate-binary-search-tree/)


## Problem {#problem}

```text
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

- The left subtree of a node contains only nodes with keys less than the node's key.
- The right subtree of a node contains only nodes with keys greater than the node's key.
- Both the left and right subtrees must also be binary search trees.

Example 1:

    2
   / \
  1   3

Input: [2,1,3]
Output: true

Example 2:

    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```


## Solution {#solution}

**Important**:

You don't only valid the current node with its left and right value.
You have to:

-   pass the new high bound for left branch, because all the values in the left branch must be less than this high bound, low bound remains
-   pass the new low bound for right branch, because all the values in the right branch must be greater than this low bound, high bound remains

<!--listend-->

```python
class Solution:
    def isValidBST(self, root):
        return self.isValidBSTBound(root, -sys.maxsize, sys.maxisze)

    def isValidBSTBound(self, root, lb, hb):
        if not root:
            return True

        if lb < root.val < hb:
            return self.isValidBSTBound(root.left, lb, root.val) and self.isValidBSTBound(root.right, root.val, hb)
        else:
            return False
```
