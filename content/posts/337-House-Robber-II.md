+++
title = "337 - House Robber III"
date = 2020-05-06T17:43:00+02:00
lastmod = 2020-05-06T18:00:21+02:00
tags = ["medium", "tree", "dp", "recursion", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/house-robber-iii/)


## Problem {#problem}

```text
The thief has found himself a new place for his thievery again. There is only one entrance to this area, called the "root." Besides the root, each house has one and only one parent house. After a tour, the smart thief realized that "all houses in this place forms a binary tree". It will automatically contact the police if two directly-linked houses were broken into on the same night.

Determine the maximum amount of money the thief can rob tonight without alerting the police.

Example 1:

Input: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \
     3   1

Output: 7
Explanation: Maximum amount of money the thief can rob = 3 + 3 + 1 = 7.
Example 2:

Input: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \
 1   3   1

Output: 9
Explanation: Maximum amount of money the thief can rob = 4 + 5 = 9.
```


## Solution {#solution}

We can do it recursively with a memo, to reduce the search depth.

On every node, we have 2 statuses, which will determine our next move:

-   Status:

    1.  Existence of current node
    2.  Wether the parent node was robbed?

    So we can define a recursive function with two parameters:

    ```python
    def robRec(root, isRobbed)
    ```

-   Transition:

    -   If parent robbed

        Then we can not rob the current node, we just sum up the result of the children

        ```python
        ans = self.robRec(root.left, False) + self.robRec(root.right, Falsek)
        ```

    -   If not robbed

        Then we have a choice: rob the current node or not.

        -   if we rob the current node

            ```python
            rob = root.val + self.robRec(root.left, True) + self.robRec(root.right, True)
            ```

        -   if we do not rob the current node

            ```python
            not_rob = self.robRec(root.left, False) + self.robRec(root.right, True)
            ```

    And we have to choose the greater one

    ```python
    ans = max(rob, not_rob)
    ```

-   Initial state

    ```python
    root = root
    isRobbed = False
    ```

<!--listend-->

```python
class Solution:
    memo = {}
    def rob(self, root):
        return self.robRec(root, False)

    def robRec(self, root, isRobbed):
        if not root:
            return 0

        if (root, isRobbed) in memo:
            return memo[(root, isRobbed)]

        if isRobbed:
            ans = self.robRec(root.left, False) + self.robRec(root.right, False)
        else:
            ans = max(root.val + self.robRec(root.left, True) + self.robRec(root.right, True),
                      self.robRec(root.left, False) + self.robRec(root.right, False))

        memo[(root, isRobbed)] = ans

        return ans
```
