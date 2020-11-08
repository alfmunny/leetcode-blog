+++
title = "404 - Sum of Left Leaves"
date = 2020-08-24T22:57:00+02:00
lastmod = 2020-08-24T22:58:55+02:00
tags = ["easy", "tree", "dfs", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/sum-of-left-leaves/)


## Problem {#problem}

```text
Find the sum of all left leaves in a given binary tree.

Example:

    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.
```


## Solution {#solution}

```python
class Solution:
    def sumOfLeftLeaves(self, root: TreeNode) -> int:
        return self.dfs(root, 0, False)

    def dfs(self, root, presum, isLeft):
        if not root:
            return 0
        if not root.left and not root.right and isLeft:
            return presum + root.val
        else:
            return self.dfs(root.left, presum, True) + self.dfs(root.right, presum, False)
```
