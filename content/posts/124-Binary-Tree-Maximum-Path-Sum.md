+++
title = "124 - Binary Tree Maximum Path Sum"
date = 2020-04-29T16:49:00+02:00
lastmod = 2020-04-29T16:51:13+02:00
tags = ["hard", "tree", "dfs", "recursion", "1-pass", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/binary-tree-maximum-path-sum/)


## Problem {#problem}

Given a non-empty binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

Example 1:

Input: [1,2,3]

  1
 / \\
2   3

Output: 6
Example 2:

Input: [-10,9,20,null,null,15,7]

 -10
 / \\
9  20
  /  \\
 15   7

Output: 42


## Solution {#solution}

**Important**:

Remember we should find a path, not a sub tree.


### Solution 1: Hash {#solution-1-hash}

```python
from collections import defaultdict

class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

class Solution:
    h = defaultdict(int)

    def maxPathSum(self, root: TreeNode) -> int:
        if not root:
            return -sys.maxsize

        return max(self.maxPathSumFrom(root), self.maxPathSum(root.left),
                   self.maxPathSum(root.right))

    def maxPathSumFrom(self, root):

        if not root:
            return 0

        return max(
            root.val, root.val + self.maxPathSumDfs(root.right),
            root.val + self.maxPathSumDfs(root.left), root.val +
            self.maxPathSumDfs(root.right) + self.maxPathSumDfs(root.left))

    def maxPathSumDfs(self, root):
        if not root:
            return 0

        if root in self.h:
            return self.h[root]
        else:
            rightSum = self.h.get(root.right, self.maxPathSumDfs(root.right))
            leftSum = self.h.get(root.left, self.maxPathSumDfs(root.left))
            ans = max(root.val, root.val + rightSum, root.val + leftSum)
            self.h[root] = ans

        return ans
```


### Solution 2: Global maximum with dfs {#solution-2-global-maximum-with-dfs}

The tricky part here is to update the global maximum always with both left branch and right branch,
but dfs only returns with the larger branch of the node, because we have to keep the left and right side as a "path" not a "tree

Version 1:

```python
class Solution:
    ans = -sys.maxsize

    def maxPathSum(self, root):
        self.dfs(root)
        return self.ans

    def dfs(self, root):
        if not root:
            return 0

        left = max(self.dfs(root.left), 0)
        right = max(self.dfs(root.right), 0)

        self.ans = max(self.ans, root.val + left + right)
        return root.val + max(left, right)
```

Version 2: I find it easier to understand

```python
class Solution:
    ans = -sys.maxsize

    def maxPathSum(self, root):
        self.dfs(root)
        return self.ans

    def dfs(self, root):
        if not root:
            return 0

        left = self.dfs(root.left)
        right = self.dfs(root.right)

        val = max(root.val, root.val + left, root.val + right)
        self.ans = max(self.ans, val, root.val + left + right)

        return val
```
