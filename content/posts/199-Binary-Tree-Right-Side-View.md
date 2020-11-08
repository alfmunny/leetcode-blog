+++
title = "199 - Binary Tree Right Side View"
date = 2020-08-23T17:44:00+02:00
lastmod = 2020-08-23T17:45:31+02:00
tags = ["medium", "dfs", "tree", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/binary-tree-right-side-view/)


## Problem {#problem}

```text
Given a binary tree, imagine yourself standing on the right side of it, return the values of the nodes you can see ordered from top to bottom.

Example:

Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---
```


## Solution {#solution}

Comprare the depth. DFS.

Keep track of the current depth.
And the length of current answer is the previous depth.

Traverse right to left

If current\_depth > previous depth, then it appears in the right view.

```python
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        ans = []
        self.print(root, ans, 0)
        return ans

    def print(self, root, ans, depth):
        if not root:
            return

        if depth + 1 > len(ans): ans.append(root.val)

        self.print(root.right, ans, depth+1)
        self.print(root.left, ans, depth+1)
```
