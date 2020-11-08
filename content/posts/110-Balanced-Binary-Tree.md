+++
title = "110 - Balanced Binary Tree"
date = 2020-08-19T11:21:00+02:00
lastmod = 2020-08-19T11:25:46+02:00
tags = ["easy", "tree", "1-pass", "dfs"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/balanced-binary-tree/)


## Problem {#problem}

```text
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

Example 1:

Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
Return true.

Example 2:

Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.
```


## Solution {#solution}


### Solution 1: multiple pass {#solution-1-multiple-pass}

```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        if not root:
            return True

        hr = self.height(root.right)
        hl = self.height(root.left)

        return self.isBalanced(root.right) and self.isBalanced(
            root.left) and abs(hr - hl) <= 1

    def height(self, root):
        if not root:
            return 0
        return 1 + max(self.height(root.right), self.height(root.left))
```

This method has to calculate the height mutiple times, which costs a lot of time.


### Solution 2: one pass {#solution-2-one-pass}

It is a dfs method, which only go over all nodes one time.

```python
class Solution:
    def isBalanced(self, root: TreeNode) -> bool:
        return self.height(root) != -1

    def height(self, root):
        if not root:
            return 0
        lh = self.height(root.right)
        if lh == -1:
            return -1
        rh = self.height(root.left)
        if rh == -1:
            return -1
        if abs(lh - rh) > 1:
            return -1
        return max(lh, rh) + 1
```
