+++
title = "61 - Rotate List"
date = 2020-06-18T14:10:00+02:00
lastmod = 2020-06-18T14:11:59+02:00
tags = ["medium", "list", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/rotate-list/)


## Problem {#problem}

```text
Given a linked list, rotate the list to the right by k places, where k is non-negative.

Example 1:

Input: 1->2->3->4->5->NULL, k = 2
Output: 4->5->1->2->3->NULL
Explanation:
rotate 1 steps to the right: 5->1->2->3->4->NULL
rotate 2 steps to the right: 4->5->1->2->3->NULL

Example 2:

Input: 0->1->2->NULL, k = 4
Output: 2->0->1->NULL
Explanation:
rotate 1 steps to the right: 2->0->1->NULL
rotate 2 steps to the right: 1->2->0->NULL
rotate 3 steps to the right: 0->1->2->NULL
rotate 4 steps to the right: 2->0->1->NULL
```


## Solution {#solution}

Note: k may be larger than the total count of nodes. We sould preprocess k first

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def rotateRight(self, head: ListNode, k: int) -> ListNode:
        if not head or not k:
            return head

        first = second = head

        count = 0

        while first:
            count += 1
            first = first.next

        k = k % count
        first = head

        for i in range(k):
            first = first.next

        while first.next:
            first = first.next
            second = second.next

        first.next = head
        head = second.next
        second.next = None

        return head
```
