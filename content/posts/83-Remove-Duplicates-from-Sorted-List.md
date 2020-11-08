+++
title = "83 - Remove Duplicates from Sorted List"
date = 2020-06-20T01:42:00+02:00
lastmod = 2020-06-20T01:42:48+02:00
tags = ["easy", "list", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)


## Problem {#problem}

```text
Given a sorted linked list, delete all duplicates such that each element appear only once.

Example 1:

Input: 1->1->2
Output: 1->2
Example 2:

Input: 1->1->2->3->3
Output: 1->2->3
```


## Solution {#solution}

```python
class Solution:
    def deleteDuplicates(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        first = head
        second = first.next

        while second:
            if first.val == second.val:
                first.next = second.next
                second = first.next
            else:
                first, second = second, second.next

        return head
```
