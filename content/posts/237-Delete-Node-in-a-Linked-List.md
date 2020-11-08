+++
title = "237 - Delete Node in a Linked List"
date = 2020-06-03T01:16:00+02:00
lastmod = 2020-06-03T01:17:47+02:00
tags = ["easy", "list", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/delete-node-in-a-linked-list/)


## Problem {#problem}

```text
Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Given linked list -- head = [4,5,1,9], which looks like following:

Example 1:

Input: head = [4,5,1,9], node = 5
Output: [4,1,9]
Explanation: You are given the second node with value 5, the linked list should become 4 -> 1 -> 9 after calling your function.

Example 2:

Input: head = [4,5,1,9], node = 1
Output: [4,5,9]
Explanation: You are given the third node with value 1, the linked list should become 4 -> 5 -> 9 after calling your function.
```


## Solution {#solution}

```python
class Solution:
    def deleteNode(self, node):
        node.val = node.next.val
        node.next = node.next.next
```
