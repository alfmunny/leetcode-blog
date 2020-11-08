+++
title = "113 - Path Sum II"
date = 2020-06-17T23:51:00+02:00
lastmod = 2020-06-17T23:52:57+02:00
tags = ["medium", "tree", "dfs", "backtrack", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/path-sum-ii/)


## Problem {#problem}

```text
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

Note: A leaf is a node with no children.

Example:

Given the below binary tree and sum = 22,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \    / \
7    2  5   1
Return:

[
   [5,4,11,2],
   [5,8,4,5]
]
```


## Solution {#solution}

```python
class Solution:
    def pathSum(self, root: TreeNode, sum: int) -> List[List[int]]:

        ans = []
        self.dfs(root, sum, [], ans)
        return ans

    def dfs(self, root, sum, path, ans):

        if not root:
            return

        path.append(root.val)
        if root.val == sum and not root.right and not root.left:
            ans.append(list(path))
        self.dfs(root.left, sum - root.val, path, ans)
        self.dfs(root.right, sum - root.val, path, ans)
        path.pop()
```
