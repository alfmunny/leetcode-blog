+++
title = "1009 - Complement of Base 10 Integer"
date = 2020-05-04T17:59:00+02:00
lastmod = 2020-05-04T18:02:50+02:00
tags = ["easy", "bit", "1-pass"]
categories = ["leetcode"]
draft = false
+++

[leetcode](https://leetcode.com/problems/complement-of-base-10-integer/)


## Problem {#problem}

```text
Every non-negative integer N has a binary representation.  For example, 5 can be represented as "101" in binary, 11 as "1011" in binary, and so on.  Note that except for N = 0, there are no leading zeroes in any binary representation.

The complement of a binary representation is the number in binary you get when changing every 1 to a 0 and 0 to a 1.  For example, the complement of "101" in binary is "010" in binary.

For a given number N in base-10, return the complement of it's binary representation as a base-10 integer.

Example 1:

Input: 5
Output: 2
Explanation: 5 is "101" in binary, with complement "010" in binary, which is 2 in base-10.

Example 2:

Input: 7
Output: 0
Explanation: 7 is "111" in binary, with complement "000" in binary, which is 0 in base-10.

Example 3:

Input: 10
Output: 5
Explanation: 10 is "1010" in binary, with complement "0101" in binary, which is 5 in base-10.
```


## Solution {#solution}


### Solution 1: XOR {#solution-1-xor}

Watch out the corner case when num is 0.

```python
class Solution:
    def bitwiseComplement(self, num: int) -> int:
        if num == 0:
            return 1

        c = 1
        n = num
        while n:
            c *= 2
            n >>= 1

        return num ^ (c - 1)
```


### Solution 2: {#solution-2}

`x = 2 * x + 1`

```text
1 = 1
1*2 + 1 = 3 = 11
3*2 + 1 = 7 = 111
7*2 + 1 = 15 = 1111
```

```python
class Solution:
    def bitwiseComplement(self, num):
        x = 1
        while x < num: x = 2 * x + 1
        return x - num
```
