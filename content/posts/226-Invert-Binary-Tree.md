+++
title = "226 - Invert Binary Tree"
date = 2020-06-01T23:36:00+02:00
lastmod = 2020-06-01T23:37:25+02:00
tags = ["easy", "tree", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/invert-binary-tree/)


## Problem {#problem}

```text
Invert a binary tree.

Example:

Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1
```


## Solution {#solution}

```python
class Solution:
    def invertTree(self):
        if root:
            tmp = root.left
            root.left = self.invertTree(root.right)
            root.right = self.invertTree(tmp)
        return root
```
