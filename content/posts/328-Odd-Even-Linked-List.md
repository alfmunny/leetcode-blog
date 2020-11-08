+++
title = "328 - Odd Even Linked List"
date = 2020-05-16T17:58:00+02:00
lastmod = 2020-05-16T17:59:11+02:00
tags = ["medium", "list", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/odd-even-linked-list/)


## Problem {#problem}

```text
Given a singly linked list, group all odd nodes together followed by the even nodes.
Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

Example 1:

Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL

Example 2:

Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL
Note:

The relative order inside both the even and odd groups should remain as it was in the input.
The first node is considered odd, the second node even and so on ...
```


## Solution {#solution}

```python
class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if not head or not head.next or not head.next.next:
            return head

        p1, p2 = head, head.next
        even = p2

        while p2 and p2.next:
            p1.next = p2.next
            p1 = p1.next
            p2.next = p1.next
            p2 = p2.next

        p1.next = even

        return head
```
