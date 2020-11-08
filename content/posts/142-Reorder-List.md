+++
title = "142 - Reorder List"
date = 2020-08-18T01:13:00+02:00
lastmod = 2020-08-18T01:14:00+02:00
tags = ["medium", "list", "sort", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/reorder-list/)


## Problem {#problem}

```text
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:

Given 1->2->3->4, reorder it to 1->4->2->3.
Example 2:

Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```


## Solution {#solution}

```python
class Solution:
    def reorderList(self, head: ListNode) -> None:
        if not head or not head.next:
            return
        fast = slow = head

        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next

        p1, p2 = slow, slow.next
        slow.next = None

        while p2:
            p2.next, p2, p1 = p1, p2.next, p2

        first = head
        tail = p1

        while tail and first:

            first.next, tail.next, first, tail = tail, first.next, first.next, tail.next
```
