+++
title = "Cousins in Binary Tree"
date = 2020-05-07T21:54:00+02:00
lastmod = 2020-05-07T21:55:35+02:00
tags = ["medium", "tree", "recursion", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/explore/featured/card/may-leetcoding-challenge/534/week-1-may-1st-may-7th/3322/)


## Problem {#problem}

```text

In a binary tree, the root node is at depth 0, and children of each depth k node are at depth k+1.

Two nodes of a binary tree are cousins if they have the same depth, but have different parents.

We are given the root of a binary tree with unique values, and the values x and y of two different nodes in the tree.

Return true if and only if the nodes corresponding to the values x and y are cousins.

Example 1:

Input: root = [1,2,3,4], x = 4, y = 3
Output: false
Example 2:

Input: root = [1,2,3,null,4,null,5], x = 5, y = 4
Output: true
Example 3:

Input: root = [1,2,3,null,4], x = 2, y = 3
Output: false

Note:

The number of nodes in the tree will be between 2 and 100.
Each node has a unique integer value from 1 to 100.
```


## Solution {#solution}

-   depth funciton for depth comparison
-   A map for remember the parent value of the node

<!--listend-->

```python
class Solution:
    m = {}

    def isCousins(self, root, x, y):
        if not root:
            return False

        if self.depth(root, x) == self.depth(root, y):
            return self.m[x] != self.m[y]

        return False

    def depth(self, root, val):
        if not root:
            return -1

        if root.val == val:
            return 0
        else:

            left = self.depth(root.left, val)
            right = self.depth(root.right, val)

            if left >= 0:
                self.m[root.left.val] = root.val
                return 1 + left
            elif right >= 0:
                self.m[root.right.val] = root.val
                return 1 + right

        return -1
```
