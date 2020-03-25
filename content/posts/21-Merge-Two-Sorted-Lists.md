+++
title = "21 - Merge Two Sorted Lists"
date = 2020-03-25T19:55:00+01:00
lastmod = 2020-03-26T00:09:20+01:00
tags = ["easy", "list", "recursion", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/merge-two-sorted-lists/)


## Problem {#problem}

```text
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```


## Notes {#notes}

Recursion is your friend!


## Solution {#solution}


### Solution 1: Recursive {#solution-1-recursive}

```python
class Solution:
    def mergeTwoLists(self, l1, l2):
        if not l1:
            return l2
        if not l2:
            return l1

        if l1.val > l2.val:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
        else:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
```


### <span class="org-todo todo TODO">TODO</span> Solution 2: How to do it none recursively {#solution-2-how-to-do-it-none-recursively}
