+++
title = "136 - Single Number"
date = 2020-04-01T22:36:00+02:00
lastmod = 2020-05-09T16:12:49+02:00
tags = ["easy", "array", "hash", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/single-number/)


## Problem {#problem}

```text
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Example 1:

Input: [2,2,1]
Output: 1
Example 2:

Input: [4,1,2,1,2]
Output: 4
```


## Notes {#notes}


### Solution 1: Hash Table {#solution-1-hash-table}


### Solution 2: Bit manipulation {#solution-2-bit-manipulation}

Consider XOR all element together. The left number is the single number.


## Solution {#solution}


### Solution 1: Hash Table {#solution-1-hash-table}

```python
class Solution:
    def singleNumber(self, nums):
        table = {}
        for i in nums:
            table[i] = table.get(i, 0) + 1
        for k in table:
            if table[k] == 1:
                return k
```


### Solution 2: Bit manipulation for finding the single number {#solution-2-bit-manipulation-for-finding-the-single-number}

```python
class Solution:
    def singleNumber(self, nums):

        res = 0

        for i in nums:
            res ^= i

        return res

print(Solution().singleNumber([2, 2, 5, 1, 8, 1, 9, 8, 9]))
```


### Solution 3: Python reduce {#solution-3-python-reduce}

```python
from functools import reduce
import operator
nums = [2, 2, 5, 1, 8, 1, 9, 8, 9]
print(reduce(lambda x, y: x ^ y, nums))
print(reduce(operator.xor, nums))
```
