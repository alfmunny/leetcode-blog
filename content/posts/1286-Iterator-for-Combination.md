+++
title = "1286 - Iterator for Combination"
date = 2020-08-27T00:12:00+02:00
lastmod = 2020-08-27T00:35:14+02:00
tags = ["medium", "bit", "dfs", "1-hint"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/iterator-for-combination/)


## Problem {#problem}

```text
Design an Iterator class, which has:

A constructor that takes a string characters of sorted distinct lowercase English letters and a number combinationLength as arguments.
A function next() that returns the next combination of length combinationLength in lexicographical order.
A function hasNext() that returns True if and only if there exists a next combination.


Example:

CombinationIterator iterator = new CombinationIterator("abc", 2); // creates the iterator.

iterator.next(); // returns "ab"
iterator.hasNext(); // returns true
iterator.next(); // returns "ac"
iterator.hasNext(); // returns true
iterator.next(); // returns "bc"
iterator.hasNext(); // returns false


Constraints:

1 <= combinationLength <= characters.length <= 15
There will be at most 10^4 function calls per test.
It's guaranteed that all calls of the function next are valid.
```


## Solution {#solution}


### Solution 1: DFS to generate the bit mask {#solution-1-dfs-to-generate-the-bit-mask}

```python
class CombinationIterator:

    def __init__(self, characters: str, combinationLength: int):
        self.bitmasks = []
        self.characters = characters
        self.combinationLength = combinationLength
        self.dfs(0, 0, [])
        print(self.bitmasks)

    def next(self) -> str:
        ans = ""
        mask = self.bitmasks.pop(0)
        for i in range(len(mask)):
            if mask[i] == "1":
                ans += self.characters[i]
        return ans

    def hasNext(self) -> bool:
        return self.bitmasks != []

    def dfs(self, count, index, path):

        if index == len(self.characters):
            if count == self.combinationLength:
                self.bitmasks.append(list(path))
            return

        for i in ["1", "0"]:
            if count == self.combinationLength and i == "1":
                continue

            path.append(i)
            if i == "1":
                self.dfs(count+1, index+1, path)
            else:
                self.dfs(count, index+1, path)

            path.pop()
```


### Solution 2: Generate the bismask iteratively {#solution-2-generate-the-bismask-iteratively}

```python
class CombinationIterator:
    def __init__(self, characters: str, combinationLength: int):
        self.characters = characters
        self.combinationLength = combinationLength
        self.bitmasks = []
        for mask in range(1 << len(characters)):
            if bin(mask).count('1') == self.combinationLength:
                res = ""
                for i in range(len(characters)):
                    res = str(mask%2) + res
                    mask >>= 1
                self.bitmasks.append(res)
        self.bitmasks = self.bitmasks[::-1]


    def next(self) -> str:
        ans = ""
        mask = self.bitmasks.pop(0)
        for i in range(len(mask)):
            if mask[i] == "1":
                ans += self.characters[i]
        return ans

    def hasNext(self) -> bool:
        return self.bitmasks != []
```
