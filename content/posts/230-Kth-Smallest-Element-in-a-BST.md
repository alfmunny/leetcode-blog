+++
title = "230 - Kth Smallest Element in a BST"
date = 2020-05-20T22:37:00+02:00
lastmod = 2020-05-20T22:45:16+02:00
tags = ["medium", "array", "tree", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)


## Problem {#problem}

```text
230. Kth Smallest Element in a BST
Medium

2239

57

Add to List

Share
Given a binary search tree, write a function kthSmallest to find the kth smallest element in it.

Note:
You may assume k is always valid, 1 ≤ k ≤ BST's total elements.

Example 1:

Input: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
Output: 1
Example 2:

Input: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
Output: 3
```


## Solution {#solution}

```python
class Solution:
    def kthSmallest(self, root):
        self.k = k
        self.ans = root.val
        traverse(root)
        return self.ans

    def traverse(self, root):
        if not root:
            return
        traverse(root.left)

        self.k -= 1
        if not self.k:
            self.ans = root.val
        else:
            traverse(root.right)
```
