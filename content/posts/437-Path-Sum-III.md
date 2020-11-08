+++
title = "437 - Path Sum III"
date = 2020-04-26T15:52:00+02:00
lastmod = 2020-04-26T15:53:39+02:00
tags = ["medium", "tree", "recursion", "1-fail"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/path-sum-iii/)


## Problem {#problem}

```text
You are given a binary tree in which each node contains an integer value.

Find the number of paths that sum to a given value.

The path does not need to start or end at the root or a leaf, but it must go downwards (traveling only from parent nodes to child nodes).

The tree has no more than 1,000 nodes and the values are in the range -1,000,000 to 1,000,000.

Example:

root = [10,5,-3,3,2,null,11,3,-2,null,1], sum = 8

      10
     /  \
    5   -3
   / \    \
  3   2   11
 / \   \
3  -2   1

Return 3. The paths that sum to 8 are:

1.  5 -> 3
2.  5 -> 2 -> 1
3. -3 -> 11
```


## Solution {#solution}

**Important**:

Three parts in recursion:

1.  the path sum of the left child
2.  the path sum of the right child
3.  the path sum only from the root

<!--listend-->

```python
class Solution:
    def pathSum(self, root, sum):
        if not root:
            return 0

        return self.pathSum(root.left, sum) + self.pathSum(
            root.right, sum) + self.pathSumFrom(root, sum)

    def pathSumFrom(self, root, sum):

        if not root:
            return 0

        if root.val == sum:
            return 1 + self.pathSumFrom(root.left, 0) + self.pathSumFrom(
                root.right, 0)
        else:
            return self.pathSumFrom(root.left,
                                    sum - root.val) + self.pathSumFrom(
                                        root.right, sum - root.val)
```
