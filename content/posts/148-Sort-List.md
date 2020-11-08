+++
title = "148 - Sort List"
date = 2020-08-17T16:41:00+02:00
lastmod = 2020-08-17T16:41:28+02:00
tags = ["medium", "list", "sort", "recursive", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/sort-list/)


## Problem {#problem}

```text
Sort a linked list in O(n log n) time using constant space complexity.

Example 1:

Input: 4->2->1->3
Output: 1->2->3->4
Example 2:

Input: -1->5->3->4->0
Output: -1->0->3->4->5
```


## Solution {#solution}

Merge Sort

1.  Slow-Fast-Pointer to split the list into half. Do not forget slow.next = None
2.  Sort two part recursively and merge together

<!--listend-->

```python
class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head or not head.next:
            return head

        # split in half
        fast = slow = head
        while fast.next and fast.next.next:
            fast = fast.next.next
            slow = slow.next

        second = slow.next
        slow.next = None

        first = self.sortList(head)
        second = self.sortList(second)

        # merge
        return self.merge(first, second)

    def merge(self, p1, p2):
        p = dummy = ListNode(0)

        while p1 and p2:
            if p1.val < p2.val:
                p.next, p1 = p1, p1.next
            else:
                p.next, p2 = p2, p2.next
            p = p.next

        p.next = p1 or p2

        return dummy.next
```
