+++
title = "450 - Delete Node in a BST"
date = 2020-08-31T23:38:00+02:00
lastmod = 2020-08-31T23:39:49+02:00
tags = ["medium", "tree", "recursive", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/delete-node-in-a-bst/)


## Problem {#problem}

```text
Design an Iterator class, which has:

A constructor that takes a string characters of sorted distinct lowercase English letters and a number combinationLength as arguments.
A function next() that returns the next combination of length combinationLength in lexicographical order.
A function hasNext() that returns True if and only if there exists a next combination.


Example:

CombinationIterator iterator = new CombinationIterator("abc", 2); // creates the iterator.

iterator.next(); // returns "ab"
iterator.hasNext(); // returns true
iterator.next(); // returns "ac"
iterator.hasNext(); // returns true
iterator.next(); // returns "bc"
iterator.hasNext(); // returns false


Constraints:

1 <= combinationLength <= characters.length <= 15
There will be at most 10^4 function calls per test.
It's guaranteed that all calls of the function next are valid.
```


## Solution {#solution}

```python
class Solution:
    def deleteNode(self, root: TreeNode, key: int) -> TreeNode:

        if not root:
            return None

        if root.val > key:
            root.left = self.deleteNode(root.left, key)
        elif root.val < key:
            root.right = self.deleteNode(root.right, key)
        else:
            if not root.left:
                root = root.right
            elif not root.right:
                root = root.left
            else:
                node = self.getMin(root.right)
                node.left = root.left
                root = root.right

        return root

    def getMin(self, root):
        if not root:
            return None

        return self.getMin(root.left) or root
```
