+++
title = "95 - Unique Binary Search Trees II"
date = 2020-06-20T02:56:00+02:00
lastmod = 2020-06-20T02:57:33+02:00
tags = ["medium", "tree", "recursive", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/unique-binary-search-trees-ii/)


## Problem {#problem}

```text
Given an integer n, generate all structurally unique BST's (binary search trees) that store values 1 ... n.

Example:

Input: 3
Output:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
Explanation:
The above output corresponds to the 5 unique BST's shown below:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```


## Solution {#solution}

```python
class Solution:
    def generateTrees(self, n: int) -> List[TreeNode]:
        if n == 0:
            return []
        return self.helper(1, n+1)

    def helper(self, start, end):
        if start >= end:
            return [None]
        res = []
        for i in range(start, end):
            for left in self.helper(start, i):
                for right in self.helper(i+1, end):
                    node = TreeNode(i)
                    node.left, node.right = left, right
                    res.append(node)
        return res
```
