+++
title = "876 - Middle of the Linked List"
date = 2020-04-08T11:28:00+02:00
lastmod = 2020-04-08T23:29:18+02:00
tags = ["easy", "array", "two-pointer", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/middle-of-the-linked-list/)


## Problem {#problem}

```text
Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.



Example 1:

Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.
Example 2:

Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
```


## Solution {#solution}


### Solution 1: two-pointer {#solution-1-two-pointer}

```python
class Solution:
    def middleNode(self, head: ListNode) -> ListNode:
        p1 = p2 = head
        while p2 and p2.next:
            p2 = p2.next.next
            p1 = p1.next

        return p1
```


### Solution 2: counter {#solution-2-counter}

```python
class Solution:
    def middleNode(self, head):
        mid = head
        count = 0
        while head:
            count += 1
            if count % 2 == 0:
                mid = mid.next
            head = head.next
        return mid
```
