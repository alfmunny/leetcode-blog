+++
title = "109 - Convert Sorted List to Binary Search Tree"
date = 2020-08-18T16:24:00+02:00
lastmod = 2020-08-18T20:52:40+02:00
tags = ["medium", "list", "dfs", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/convert-sorted-list-to-binary-search-tree/)


## Problem {#problem}

```text
Given the head of a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
```


## Solution {#solution}

```python
class Solution:
    def sortedListToBST(self, head: ListNode) -> TreeNode:
        if not head:
            return None
        if not head.next:
            return TreeNode(head.val)

        pre, slow, fast = None, head, head

        while fast and fast.next:
            pre, slow, fast = slow, slow.next, fast.next.next

        pre.next = None
        root = TreeNode(slow.val)
        root.left = self.sortedListToBST(head)
        root.right = self.sortedListToBST(slow.next)

        return root
```
