+++
title = "460 - LFU Cache"
date = 2020-04-26T00:38:00+02:00
lastmod = 2020-04-26T00:49:23+02:00
tags = ["hard", "design", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/lfu-cache/)


## Problem {#problem}

```text
Design and implement a data structure for Least Frequently Used (LFU) cache. It should support the following operations: get and put.

get(key) - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
put(key, value) - Set or insert the value if the key is not already present. When the cache reaches its capacity, it should invalidate the least frequently used item before inserting a new item. For the purpose of this problem, when there is a tie (i.e., two or more keys that have the same frequency), the least recently used key would be evicted.

Note that the number of times an item is used is the number of calls to the get and put functions for that item since it was inserted. This number is set to zero when the item is removed.



Follow up:
Could you do both operations in O(1) time complexity?



Example:

LFUCache cache = new LFUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.get(3);       // returns 3.
cache.put(4, 4);    // evicts key 1.
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```


## Solution {#solution}

1.  O(1) get => Hash table for all nodes
2.  for keeping the oder by frequency, we can have another hash table. the key is the frequency. the value is a double linked list
3.  We need a min\_freqeuncy to find the list of min frequency in O(1), and delete the last element of the list

<!--listend-->

```python
class Node:
    def __init__(self, key, value):
        self.freq = 1
        self.key = key
        self.value = value
        self.next = None
        self.prev = None


class DoubleLinkedList:
    def __init__(self):
        self._head = Node(0, 0)
        self._tail = Node(0, 0)
        self._head.next = self._tail
        self._tail.prev = self._head
        self._size = 0

    def append(self, node):
        self._connect(node, self._head.next)
        self._connect(self._head, node)
        self._size += 1

    def pop(self, node):
        self._connect(node.prev, node.next)
        node.next = None
        node.prev = None
        self._size -= 1
        return node

    def pop_last(self):
        return self.pop(self._tail.prev)

    def get_size(self):
        return self._size

    def _connect(self, p, n):
        p.next, n.prev = n, p


class LFUCache:
    def __init__(self, capacity):
        self.nodes = {}
        self.freq = {}
        self.min_freq = 1
        self.capacity = capacity

    def get(self, key):
        if key in self.nodes:
            node = self.nodes[key]
            l = self.freq[node.freq]
            l.pop(node)
            if l.get_size() == 0 and self.min_freq == node.freq:
                self.min_freq += 1

            node.freq += 1
            if self.freq.get(node.freq):
                self.freq[node.freq].append(node)
            else:
                l = DoubleLinkedList()
                l.append(node)
                self.freq[node.freq] = l
            return node.value
        else:
            return -1

    def put(self, key, value):

        if self.capacity == 0:
            return

        if key in self.nodes:
            self.nodes[key].value = value
            self.get(key)
        else:
            node = Node(key, value)
            if len(self.nodes) == self.capacity:
                l = self.freq[self.min_freq]
                n = l.pop_last()
                self.nodes.pop(n.key)

            self.nodes[key] = node

            if 1 in self.freq:
                self.freq[1].append(node)
            else:
                l = DoubleLinkedList()
                l.append(node)
                self.freq[1] = l
            self.min_freq = 1


c = LFUCache(3)
c.put(1, 1)
c.put(2, 2)
print(c.get(1))
print(c.get(2))
print(c.get(1))
c.put(3, 3)
print(c.get(2))
print(c.get(3))
c.put(4, 4)

print(c.get(4))
```
