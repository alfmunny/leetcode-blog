+++
title = "146 - LRU Cache"
date = 2020-04-25T00:17:00+02:00
lastmod = 2020-04-26T00:52:35+02:00
tags = ["medium", "design", "hash", "list", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/lru-cache/)


## Problem {#problem}

```text
Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a positive capacity.

Follow up:
Could you do both operations in O(1) time complexity?

Example:

LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```


## Solution {#solution}

1.  How to manage to have a O(1) for get()?

    Hash Table

2.  How to manage to have a O(1) for put()?

    We have to somehow maintain its order, when something is added.

    Linked list would come to mind at first. But how we can change its order when we call get() on a node
    and also be able to delete the last one. We would like to know the previous one of a node.

    A **Double Linked List** is a perfect match.

<!--listend-->

```python
class LRUCache:

    def __init__(self, capacity: int):
        self.count = 0
        self.capacity = capacity
        self.hash = {}
        self.head = Node(0, 0)
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    def get(self, key: int) -> int:
        if key in self.hash:
            node = self.hash[key]
            self._remove(node)
            self._add(node)
            return node.value
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key not in self.hash:
            node = Node(key, value)
            self.hash[key] = node
            self.count += 1
            self._add(node)
        else:
            node = self.hash[key]
            node.value = value
            self.get(key)

        if self.count > self.capacity:
            n = self.tail.prev
            self.hash.pop(n.key)
            self._remove(n)
            self.count -= 1

    def _connect(self, p, n):
        p.next, n.prev = n, p

    def _add(self, n):
        tmp = self.head.next
        self._connect(self.head, n)
        self._connect(n, tmp)

    def _remove(self, node):
        self._connect(node.prev, node.next)



class Node:
    def __init__(self, key, value):
        self.key = key
        self.value =  value
        self.prev = None
        self.next = None


# Your LRUCache object will be instantiated and called as such:
# obj = LRUCache(capacity)
# param_1 = obj.get(key)
# obj.put(key,value)
```
