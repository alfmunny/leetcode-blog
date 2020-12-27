+++
title = "381 - Insert Delete GetRandom O(1) - Duplicates allowed"
date = 2020-11-27T23:14:00+01:00
lastmod = 2020-11-28T00:23:36+01:00
tags = ["hard", "array", "hash", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/insert-delete-getrandom-o1-duplicates-allowed/)


## Problem {#problem}

```text
Design a data structure that supports all following operations in average O(1) time.

Note: Duplicate elements are allowed.
insert(val): Inserts an item val to the collection.
remove(val): Removes an item val from the collection if present.
getRandom: Returns a random element from current collection of elements. The probability of each element being returned is linearly related to the number of same value the collection contains.
Example:

// Init an empty collection.
RandomizedCollection collection = new RandomizedCollection();

// Inserts 1 to the collection. Returns true as the collection did not contain 1.
collection.insert(1);

// Inserts another 1 to the collection. Returns false as the collection contained 1. Collection now contains [1,1].
collection.insert(1);

// Inserts 2 to the collection, returns true. Collection now contains [1,1,2].
collection.insert(2);

// getRandom should return 1 with the probability 2/3, and returns 2 with the probability 1/3.
collection.getRandom();

// Removes 1 from the collection, returns true. Collection now contains [1,2].
collection.remove(1);

// getRandom should return 1 and 2 both equally likely.
collection.getRandom();
```


## Solution {#solution}

Notes:

Remove is tricky.

1.  Find the index of the element to remove in Hash.
2.  Replace the element with the last element in array, and pop the last one.
3.  Don't forget to update the index of copied element in Hash.
4.  You have to firstly add the new index and then delete. There is a corner case when there is only one element. If you delete it first and then add, the same index is added back to hash.

<!--listend-->

```python
class RandomizedCollection:

    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.list = []
        self.dict = defaultdict(set)

    def insert(self, val: int) -> bool:
        """
        Inserts a value to the collection. Returns true if the collection did not already contain the specified element.
        """
        self.list.append(val)
        if val not in self.dict:
            ret = True
        else:
            ret = False
        self.dict[val].add(len(self.list) - 1)
        return ret


    def remove(self, val: int) -> bool:
        """
        Removes a value from the collection. Returns true if the collection contained the specified element.
        """
        if self.dict[val]:
            rm_index = self.dict[val].pop()
            last = self.list[-1]
            self.list[rm_index] = last
            self.dict[last].add(rm_index)
            self.dict[last].discard(len(self.list) - 1)
            self.list.pop()
            return True
        else:
            return False

    def getRandom(self) -> int:
        """
        Get a random element from the collection.
        """
        return random.choice(self.list)


# Your RandomizedCollection object will be instantiated and called as such:
# obj = RandomizedCollection()
# param_1 = obj.insert(val)
# param_2 = obj.remove(val)
# param_3 = obj.getRandom()
```
